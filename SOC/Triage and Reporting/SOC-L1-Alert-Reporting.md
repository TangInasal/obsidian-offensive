## Report Format

 Five Ws  approach and include at least these items in the report:

- **Who**: Which user logs in, runs the command, or downloads the file
- **What**: What exact action or event sequence was performed
- **When**: When exactly did the suspicious activity start and ended
- **Where**: Which device, IP, or website was involved in the alert
- **Why**: The most important W, the reasoning for your final verdict


## Escalation Guide
You should escalate the alerts if:
1. The alert is an indicator of a major cyberattack requiring deeper investigation or DFIR
2. Remediation actions like malware removal, host isolation, or password reset are required
3. Communication with customers, partners, management, or law enforcement agencies is required
4. You just do not fully understand the alert and need some help from more senior analysts

## Escalation Steps

To escalate the alert, in most cases, all you have to do is to **reassign the alert to the L2 on shift** and ping them in corporate chat or in person. In some teams though, you may be required to create a formal written escalation request with dozens of required fields.

No matter what the agreements are, L2 will eventually receive the ticket from you, read your report, and contact you in case of any questions. Once everything is clear, the L2 analyst will typically research the alert details further, validate if the alert is indeed a True Positive, communicate with other departments if needed, and, for major incidents, start a formal Incident Response process.

**SOC Dashboard Escalation Procedure**

1. Write an alert report and provide your verdict; move the alert to In Progress status
2. Assign the alert to your L2 on shift. L2 will receive a notification and start from your report

![[Pasted image 20250904230648.png]]

![[Pasted image 20250904230831.png]]


## Communication Cases

- **You need to escalate an urgent, critical alert, but L2 is unavailable and does not respond for 30 minutes.**  
    Ensure you know where to find emergency contacts. First, try to call L2, then L3, and finally your manager.
    
- **The alert about Slack/Teams account compromise requires you to validate the login with the affected user.**  
    Do not contact the user through the breached chat - use alternative contact methods like a phone call.
    
- **You receive an overwhelming number of alerts during a short period of time, some of which are critical.**  
    Prioritise the alerts according to the workflow, but inform your L2 on shift about the situation.
    
- **After a few days, you realise that you misclassified the alert and likely missed a malicious action.**  
    Immediately reach out to your L2 explaining your concerns. Threat actors can be silent for weeks before impact.
    
- **You can not complete the alert triage since the SIEM logs are not parsed correctly or are not searchable.**  
    Do not skip the alert - investigate what you can and report the issue to your L2 on shift or SOC engineer.
