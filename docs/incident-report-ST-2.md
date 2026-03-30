# Incident Report — ST-2

## Incident Title
Suspicious Login Detected from Unknown IP – Investigation & Firewall Block Required

## Summary
A successful login event was detected from source IP **192.168.213.129** on host **Windows11**. Based on the related failed login activity from the same IP, this event is suspicious and may indicate compromised credentials.

## Classification
- **Event ID:** 4624
- **Category:** Successful Authentication
- **Attack Type:** Suspected successful brute-force / unauthorized access
- **Severity:** Highest
- **Status:** Investigation

## Affected Asset
- **Host:** Windows11
- **Source IP:** 192.168.213.129

## Evidence
- Event Code **4624** visible in Jira ticket
- Same source IP previously associated with repeated failed logins
- Jira labels include:
  - Block
  - Firewall
  - IP
  - Incident
  - Malicious
  - Security

## Security Impact
A successful login after repeated failed attempts raises the risk of unauthorized access and potential account compromise.

## L1 Triage
- Verified the alert details
- Confirmed the source IP was suspicious
- Routed the case for investigation

## L2 Investigation
- Compared the successful login event against the failed login pattern
- Determined the same source IP is likely responsible for both phases
- Recommended immediate containment due to compromise risk

## Recommended Actions
1. Block **192.168.213.129** at firewall level
2. Reset affected account credentials
3. Review login history for the impacted account
4. Check the host for persistence or follow-on activity
5. Document all findings in the case record

## Final Assessment
**True Positive — Suspicious successful login likely related to brute-force activity**
