# Architecture

## Lab Systems

### Attacker
- **OS:** Kali Linux
- **IP:** 192.168.213.129
- **Purpose:** Initiate RDP login attempts against Windows host

### Victim
- **OS:** Windows 11
- **IP:** 192.168.213.130
- **Purpose:** Generate Windows security events for failed and successful authentication

### SIEM
- **Platform:** Splunk Enterprise
- **IP:** 192.168.213.132
- **Purpose:** Collect, search, detect, and alert on security logs

### Ticketing
- **Platform:** Jira
- **Purpose:** Manage SOC workflow, assign status, track investigation and resolution

---

## Data Flow

1. Kali initiates repeated RDP authentication attempts.
2. Windows 11 records Event ID 4625 for failed logins.
3. After successful authentication, Windows records Event ID 4624.
4. Logs are available to Splunk for analysis.
5. Splunk scheduled alerts trigger when thresholds and correlation logic are met.
6. Jira tickets document the alert and investigation process.
7. SOC analysts move tickets through triage, investigation, escalation, and resolution.
