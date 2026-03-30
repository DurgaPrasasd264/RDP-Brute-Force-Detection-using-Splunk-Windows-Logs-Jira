# Screenshot Analysis

## 1. Jira Kanban Board
This screenshot shows the SOC ticketing workflow implemented in Jira.

### Workflow states observed
- New Alert
- Triage
- Investigation
- Escalated
- Resolved

### Security meaning
This reflects a realistic incident handling process where alerts are reviewed, investigated, escalated if needed, and closed after resolution.

---

## 2. Splunk Triggered Alerts
This screenshot shows the Splunk Triggered Alerts page.

### Key observations
- Total results displayed: **101**
- Alerts shown include:
  - Failed Login Attempts
  - Successful Login Occur
- Severity shown:
  - Medium for failed login alert
  - High for successful login alert

### Security meaning
Repeated failed logins suggest brute-force behavior. A successful login from the same activity chain suggests possible credential compromise.

---

## 3. Splunk Alert Configuration
This screenshot shows four enabled alerts:
- Failed Login Attempt
- Failed Login Attempts
- RDP brute force detection
- Successful Login Occur

### Security meaning
The alert set demonstrates both threshold-based and attack-specific detection engineering.

---

## 4. Kali FreeRDP Screenshot
This screenshot shows a successful remote session from Kali to **192.168.213.130** using FreeRDP.

### Security meaning
This is evidence of successful access to the victim system. In the context of repeated failed logins, it supports the suspicious login finding.

---

## 5. Jira Suspicious Login Ticket
This ticket documents a successful login event.

### Details shown
- Event Code: **4624**
- Host: **Windows11**
- Source IP: **192.168.213.129**
- Status: **Investigation**
- Priority: **Highest**
- Action requested: investigate and block the IP at firewall level

### Security meaning
This is the higher severity event because the attack may have moved from attempts to actual access.

---

## 6. Jira Failed Login Ticket
This ticket documents repeated failed login attempts.

### Details shown
- Event ID: **4625**
- Source IP: **192.168.213.129**
- Target system: **Windows 11**
- Status: **Escalated**
- Priority: **Medium**

### Security meaning
This ticket captures the brute-force phase before confirmed success.

---

## Overall Finding
The screenshots together show a complete SOC workflow:
1. Attack simulation
2. Log generation
3. Splunk detection
4. Alert trigger
5. Jira ticket creation
6. Triage and escalation
7. Investigation and containment recommendation
