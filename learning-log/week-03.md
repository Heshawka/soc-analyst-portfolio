7/23/26

This week is gonna be a bit different that the past few. LetsDefend has stopped giving any alerts, which is probably because I'm not paying for the highest tier subscription. This means our usual 3 alert budget for each day isn't sustainable. I will still convert some drafts into polished ones for the portfolio, but our main focus will start to shift more towards learning Splunk and using it in my homelab/BOTS challenge. 

-Today's focus is mainly learning SPL and going through the official Splunk search tutorial. Also planning on applying to some more positions today.

Splunk Search Tutorial: https://help.splunk.com/en/splunk-enterprise/search/search-tutorial/9.4/introduction/about-the-search-tutorial

NOTES: 

• If you know when an alert may have fired, time range can be really helpful

Searching the tutorial data:

• Used buttercupgames (error OR fail* OR severe) to search for the terms error, fail, or severe in events that also mention buttercupgames. Wildcard * is used for fail, failed, failure, etc.
buttercupgames (error OR fail* OR severe).

• Precedence for expressions: () -> NOT -> OR -> AND

• Learned search basics like index, sourcetype, EventCode, boolean expressions. Got some familiarity with how this works due to experience with SQL and DBMSs.

• Applying to some positions, detailed in the application tracker spreadsheet.