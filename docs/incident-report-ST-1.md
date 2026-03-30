# Incident Report — ST-1

## Incident Title
Failed Login Attempts Detected - 192.168.213.129

## Summary
A series of failed login attempts were detected from source IP **192.168.213.129** targeting **Windows 11**. The activity is consistent with possible brute-force or password guessing behavior.

## Classification
- **Event ID:** 4625
- **Category:** Failed Authentication
- **Attack Type:** Suspected RDP brute-force
- **Severity:** Medium
- **Status:** Escalated

## Affected Asset
- **Host:** Windows 11
- **Source IP:** 192.168.213.129

## Evidence
- Multiple failed login attempts observed from the same source IP
- Alert originated from Splunk
- Jira ticket labels indicate security incident and IP block consideration

## Analyst Notes
Observed repeated authentication failures from a single source IP. The pattern suggests intentional password guessing rather than normal user behavior.

## L1 Triage
- Alert validated as relevant
- Source IP identified
- Activity classified as suspicious
- Escalated for deeper investigation

## L2 Investigation
- Correlated with additional authentication activity
- Reviewed potential relationship to successful logon event
- Determined that source IP should be treated as suspicious

## Recommended Actions
1. Block source IP **192.168.213.129**
2. Check whether the targeted account experienced a later successful login
3. Review account lockout settings
4. Monitor for repeated attempts against other usernames or hosts

## Final Assessment
**True Positive — Suspicious brute-force activity observed**
