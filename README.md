# 🛡️ SOC Mini Lab — RDP Brute Force Detection & Incident Response

> End-to-end Security Operations Center (SOC) simulation covering attack execution, SIEM detection, alerting, ticketing, and incident response (L1 & L2).

---

## 📌 Project Overview

This project demonstrates a real-world SOC workflow where a brute-force attack is detected, investigated, and mitigated using Splunk SIEM and Jira ticketing.

The lab replicates how SOC teams handle authentication-based attacks such as RDP brute-force attempts.

### 🔍 Key Highlights
- Detection of brute-force attacks using Windows logs
- Correlation of failed and successful login events
- Real-time alerting in Splunk
- SOC workflow (L1 triage → L2 investigation → response)
- Incident tracking using Jira

---

## 🏗️ Lab Architecture


Kali Linux (Attacker) ──▶ RDP Attack ──▶ Windows 11 (Victim)
192.168.213.129 192.168.213.130
│
Splunk Forwarder (Logs)
│
▼
Splunk Enterprise (SIEM)
192.168.213.132
│
Alert Triggered
│
▼
Jira Ticket Created


---

## 🧰 Tools & Technologies

| Tool | Purpose |
|------|--------|
| Kali Linux | Attack simulation (RDP brute force) |
| Windows 10/11 | Target systems generating logs |
| Ubuntu | Splunk hosting environment |
| Splunk Enterprise | Log analysis, detection & alerting |
| Jira | Incident tracking |

---

## ⚔️ Attack Scenario

- **Attack Type:** RDP Brute Force  
- **MITRE Technique:** T1110.001  
- **Protocol:** RDP (Port 3389)

### 📡 Source & Target
- Source IP: `192.168.213.129`
- Target IP: `192.168.213.130`

### 🔴 Attack Behavior
- Multiple failed login attempts (Event ID 4625)
- Successful login after brute force (Event ID 4624)

---

## 📜 Log Analysis

### ❌ Failed Login — Event ID 4625
- Indicates incorrect password attempts
- Logon Type 10 (RDP login)
- High frequency indicates brute-force attack

### ✅ Successful Login — Event ID 4624
- Indicates successful authentication
- Critical if preceded by multiple failures

---

## 🔍 Detection Engineering (Splunk SPL)

### 🚨 Brute Force Detection

```spl
index=windows_security EventCode=4625 Logon_Type=10
| stats count by src_ip, dest_host
| where count >= 5
🚨 Successful Login After Failures
index=windows_security (EventCode=4624 OR EventCode=4625)
| stats count(eval(EventCode=4625)) as failed,
        count(eval(EventCode=4624)) as success
by src_ip, user
| where failed > 5 AND success > 0
```
### 🚨 Alerting

Total Alerts Triggered: 101

Trigger Conditions:


Multiple failed login attempts detected

Successful login after brute-force activity

Severity: Medium to High

🎫 Incident Management (Jira)
```
🟡 Ticket ST-1 — Brute Force Detection

Status: Escalated

Priority: High
```

```
🔴 Ticket ST-2 — Suspicious Login

Status: Under Investigation

Priority: Critical
```

## 🧠 SOC Workflow
### 🔹 L1 Analyst (Triage)

Validate alerts

Identify suspicious IP activity

Check login patterns

Escalate to L2

### 🔹 L2 Analyst (Investigation)

Correlate Event ID 4625 and 4624

Confirm brute-force behavior

Identify compromised account

### 🔹 Indicators of Compromise (IOCs)

Source IP: 192.168.213.129

Multiple failed logins

Successful login after failures

### 🔹 Containment Actions

Block attacker IP

Reset compromised credentials

Enable account lockout policies

### 🔹 Final Verdict

True Positive — Confirmed RDP Brute Force Attack

### 🗺️ MITRE ATT&CK Mapping
Technique	Description
T1110.001	Brute Force — Password Guessing
T1021.001	Remote Services — RDP
T1078	Valid Accounts
T1190	Exploit Public-Facing Application
## 📂 Repository Structure
soc-mini-lab/
├── docs/
│   ├── architecture.png
│   ├── incident-report-ST1.md
│   └── incident-report-ST2.md
├── splunk/
│   ├── detection-rules.spl
│   └── alert-configs.conf
├── screenshots/
│   └── [lab screenshots]
└── README.md
### 📸 Screenshots

Splunk Alerts (101 triggered alerts)

Detection Rule Configuration

Kali RDP Attack Terminal

Jira Ticket Workflow

Incident Tickets (ST-1, ST-2)

### 📊 Key Outcomes

Successfully detected brute-force attack using Splunk

Generated and managed Jira tickets

Performed L1 triage and L2 investigation

Implemented full SOC workflow

Mapped attack to MITRE ATT&CK framework

### 📚 Key Learnings

Importance of Windows Event Logs (4624, 4625)

Detection logic using correlation

SIEM alert tuning

Real-world SOC investigation process

### 🚀 Future Improvements

Integrate SOAR automation

Add threat intelligence enrichment

Implement UEBA (User Behavior Analytics)

Detect lateral movement

### 👨‍💻 Author

Durga Prasad
SOC Analyst | Blue Team Enthusiast
