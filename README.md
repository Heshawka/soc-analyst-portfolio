# SOC Analyst Portfolio

Hands-on security alert triage and analysis, documented as I build toward an entry-level SOC Analyst role.

## About Me

I'm a Computer Science graduate (UC Irvine, June 2025) with a CompTIA Security+ certification (satisfies DoD 8570 IAT Level II). This repo is where I track my daily practice, document alert investigations, and build the analytical habits - clear write-ups, evidence-based reasoning, MITRE ATT&CK mapping - that the job requires.

I'm currently targeting SOC L1 roles, with a focus on DoD-adjacent contractors and MSSP/commercial SOC teams.

## What's In This Repo

### `letsdefend-writeups/`
Structured analyst write-ups from alert triage practice on [LetsDefend](https://letsdefend.io). Each write-up follows a consistent format:

- **IOCs** - indicators identified, listed up front
- **Attack Detail** - what happened, reconstructed from the evidence
- **MITRE ATT&CK Mapping** - technique(s) observed, including reasoning for false positives
- **Confidence Level / Alert Priority** 
- **Actions Taken** - steps I took to investigate the alert
- **Recommended Next Steps** - escalation guidance for L2/IR, written even when the initial access vector is unconfirmed

Fields I haven't been able to verify are marked `[confirm - X]` rather than guessed at - I'd rather flag an open question than paper over it.

### `learning-log/`
A running weekly log (`week-01.md`, `week-02.md`, etc.) of daily practice — LetsDefend alerts completed, Wireshark/Splunk/networking work, and what I learned or got stuck on. This is the raw, unpolished version behind the finished write-ups above.

## Skills Demonstrated

- Security alert triage and true/false positive determination
- MITRE ATT&CK technique mapping
- Threat intelligence enrichment (AbuseIPDB, VirusTotal IOC checks)
- Packet analysis fundamentals (Wireshark)
- Clear, structured incident documentation written for an L2/IR audience

## Contact

Open to SOC Analyst L1 opportunities - feel free to reach out via www.linkedin.com/in/angel-huertas-163966221 or angelhuertas.aah@gmail.com.