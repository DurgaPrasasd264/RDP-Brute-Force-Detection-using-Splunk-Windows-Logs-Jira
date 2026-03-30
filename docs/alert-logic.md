# Splunk Alert Logic

## Alert 1 — Failed Login Attempt
Purpose:
Detect repeated failed authentication attempts.

Why it matters:
A cluster of failed logins from one source IP often indicates password guessing.

---

## Alert 2 — Failed Login Attempts
Purpose:
Track repeated failures at a broader threshold level.

Why it matters:
This helps identify brute-force noise and recurring suspicious access attempts.

---

## Alert 3 — RDP brute force detection
Purpose:
Identify brute-force attempts specifically over RDP.

Why it matters:
RDP is a common target for unauthorized access attempts in Windows environments.

---

## Alert 4 — Successful Login Occur
Purpose:
Identify successful authentication activity.

Why it matters:
When viewed alone, a successful login may be normal. When correlated with multiple failures from the same source IP, it may indicate account compromise.

---

## Risk-Based Interpretation
- 4625 alone = suspicious but not always malicious
- multiple 4625 events from one IP = higher confidence brute-force behavior
- 4624 after repeated 4625 = highest concern because the attacker may have succeeded
