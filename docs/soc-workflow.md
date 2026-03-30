# SOC Workflow

## 1. Attack Simulation
The attack was initiated from Kali Linux against the Windows 11 target over RDP.

## 2. Log Collection
Authentication logs from Windows were ingested into Splunk.

## 3. Detection
Splunk searches looked for:
- repeated failed logins
- failed RDP login attempts
- successful logins
- successful login after multiple failures

## 4. Alert Triggering
Configured alerts were enabled and scheduled. Splunk displayed 101 triggered alerts in total.

## 5. Ticketing
Alerts were documented in Jira under a structured SOC board.

## 6. L1 Triage
L1 responsibilities:
- review ticket context
- confirm alert validity
- identify source and target
- determine if escalation is required

## 7. L2 Investigation
L2 responsibilities:
- correlate 4625 and 4624 events
- verify suspicious IP behavior
- assess risk of unauthorized access
- recommend containment

## 8. Containment and Resolution
Recommended actions:
- block 192.168.213.129 at firewall
- reset credentials
- review host for additional suspicious activity
- document final outcome
