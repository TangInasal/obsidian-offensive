
**Alert Properties**
1.  Alert Time
2. Alert Name - e.g: "Unusual Login Location" | "Potential Data Exfiltration"
3. Alert Severity - Low (Informational), Medium (Moderate), High (Severe), Critical (Urgent)
4. Alert Status - New, In-Progress, Closed
5. Alert Verdict - FP or TP
6. Alert Assignee - a.k.a Alert Owner | takes responsibility for the alert
7. Alert Description - The logic of the alert generating rule | Why can this indicate an attack
8. Alert Fields - Affected Hostname, Entered Commandline, etc


**Picking the Right Alert**
1. Filter the alerts - sort alerts by status
2. Sort by severity - sort alerts by severity
3. Sort by time - start with the oldest alerts and end with the latest ones. 

**ALERT TRIAGE**

![[Pasted image 20250903213700.png]]

**Initial Actions**
1. Filter Alerts - refer to **"Picking the right alert"**
2. Assign the alert to yourself
3. Change status to "In-progress"
4. Familiarize with the alert's details like name, description and Fields

 **Investigation**
1. Check if there is a workbook/playbook to investigate the alert
2. IF NO PLAYBOOK 
 - Understand who is under threat, like the affected user, hostname, cloud, network, or website
* Note the action described in the alert, like whether it was a suspicious login, malware, or phishing
* Look for suspicious actions shortly after or before the alert
* Use threat intelligence platforms or other available resources for verification.