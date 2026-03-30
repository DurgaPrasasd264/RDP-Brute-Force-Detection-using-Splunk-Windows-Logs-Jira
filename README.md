# 🛡️ SOC Mini Lab — RDP Brute Force Detection & Incident Response

> A hands-on Security Operations Center (SOC) project that simulates an RDP brute-force attack, collects Windows authentication logs in Splunk, triggers detections and alerts, creates Jira tickets, and follows a realistic L1/L2 incident response workflow.

---

## 📌 Project Overview

This project was built to simulate how a SOC team detects and responds to suspicious authentication activity in a Windows environment.

The lab demonstrates an end-to-end blue team workflow:

- Attack simulation from Kali Linux
- Windows log generation on victim systems
- Log forwarding and analysis in Splunk
- Alert creation and triggering in Splunk
- Ticket creation and workflow tracking in Jira
- L1 triage and L2 investigation
- Incident documentation and containment recommendations

The main attack simulated in this lab is an **RDP brute-force attack** from a Kali Linux machine against a Windows host. The attack generated both:

- **Event ID 4625** — Failed login attempts
- **Event ID 4624** — Successful login

This allowed the lab to cover both the **attack attempt phase** and the **possible account compromise phase**.

---

## 🎯 Objectives

- Simulate a real-world RDP brute-force attack in a controlled lab
- Capture authentication activity from Windows systems
- Detect failed and successful logon events in Splunk
- Build alert logic for brute-force behavior
- Use Jira to track incidents like a real SOC
- Perform L1 triage and L2 investigation
- Document the incident using professional SOC reporting style

---

## 🏗️ Lab Architecture

```text
Kali Linux (Attacker) ───────────────▶ Windows 11 (Victim)
192.168.213.129                         192.168.213.130
        │                                       │
        │                    Windows Security Logs (4625 / 4624)
        │                                       │
        └───────────────────────────────────────┘
                                                │
                                      Log Forwarding to Splunk
                                                │
                                                ▼
                                   Splunk Enterprise SIEM
                                      192.168.213.132
                                                │
                                   Detection Rules / Scheduled Alerts
                                                │
                                                ▼
                                           Jira Tickets
                                                │
                                                ▼
                                L1 Triage → L2 Investigation → Resolution


```
---

## 🧰 Tools Used

| Tool | Role |
|------|------|
| Kali Linux | Attack simulation |
| Windows 11 | Victim machine |
| Windows 10 | Additional victim |
| Ubuntu | Lab environment |
| Splunk Enterprise | SIEM detection & alerting |
| Jira | Incident ticketing |

---

## ⚔️ Attack Scenario

- **Attack Type:** RDP Brute Force  
- **Protocol:** RDP (Port 3389)  
- **Source IP:** `192.168.213.129`  
- **Target IP:** `192.168.213.130`

### Attack Flow

1. Multiple failed login attempts generated  
2. Event ID **4625** logged  
3. Successful login occurred  
4. Event ID **4624** logged  
5. Splunk detected abnormal behavior  
6. Alerts triggered  
7. Jira tickets created  

---

## 📜 Windows Security Events

### Event ID 4625 — Failed Login
- Indicates incorrect password attempts  
- Repeated failures = brute-force indicator  

### Event ID 4624 — Successful Login
- Indicates successful authentication  
- After failures = possible compromise  

---

## 🔍 Detection Engineering (Splunk)

### Failed Login Detection
```spl
index=windows_security EventCode=4625
| stats count by Source_Network_Address
| where count >= 5

```

### RDP Brute Force Detection

```
index=windows_security EventCode=4625 Logon_Type=10
| stats count by Source_Network_Address
| where count >= 5
```

### Successful Login Detection
```
index=windows_security EventCode=4624
```
### Success After Failures
```
index=windows_security (EventCode=4624 OR EventCode=4625)
| stats count(eval(EventCode=4625)) as failed,
        count(eval(EventCode=4624)) as success
by Source_Network_Address
| where failed >= 5 AND success > 0
```
---
## 🚨 Splunk Alerts

Total alerts triggered: 101
Alerts configured: 4
Alert types:
Failed Login Attempt
Failed Login Attempts
RDP brute force detection
Successful Login Occur
Why Alerts Triggered
High number of failed logins
RDP login attempts detected
Successful login after failures
Same source IP behavior

## 🎫 Jira Incident Management

Workflow
New Alert
Triage
Investigation
Escalated
Resolved
### 🟡 Ticket 1 — Failed Login Attempts
Event ID: 4625
Source IP: 192.168.213.129
Target: Windows 11
Status: Escalated
Priority: Medium

Analysis:
Multiple failed logins indicate brute-force attempt.

### 🔴 Ticket 2 — Suspicious Login
Event ID: 4624
Source IP: 192.168.213.129
Status: Investigation
Priority: Highest

Analysis:
Successful login after multiple failures → possible compromise.

## 🧠 SOC Workflow

L1 Triage
Validate alert
Identify source IP
Check event logs
Escalate if suspicious
L2 Investigation
Correlate 4625 and 4624
Analyze login behavior
Confirm attack pattern
Identify compromise
Incident Response
Block attacker IP
Reset credentials
Document findings
## 🧪 Screenshot Analysis
Jira Board

Shows SOC workflow lifecycle (New → Resolved)

Splunk Alerts
101 alerts triggered
Medium & High severity
Splunk Config
4 detection rules enabled
Kali RDP Session
Successful access to Windows machine
Jira Tickets
Failed login → Escalated
Successful login → Investigation


## 🗺️ MITRE ATT&CK Mapping
Technique	Description
T1110.001	Brute Force
T1021.001	RDP
T1078	Valid Accounts

## 📸 Screenshots



Jira SOC Board

Splunk Triggered Alerts

Splunk Alert Config

Kali RDP Session

Jira Suspicious Login

Jira Failed Login


## ✅ Key Outcomes
Detected brute-force attack using Splunk
Generated 101 alerts
Created Jira tickets
Performed L1 & L2 SOC workflow
Documented full incident lifecycle
## 📚 Key Learnings
Event correlation is critical
Failed + successful login = high risk
SIEM alerts require tuning
SOC workflow improves response
## 🚀 Future Improvements
Add SOAR automation
Integrate threat intelligence
Create Splunk dashboards
Detect lateral movement
## 💼 Resume Value
Splunk SIEM monitoring
Detection engineering
Windows log analysis
SOC L1 & L2 workflow
Incident response
## 👤 Author

Durga Prasad
SOC Analyst | Blue Team | Splunk | Incident Response


