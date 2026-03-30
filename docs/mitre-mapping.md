# MITRE ATT&CK Mapping

## T1110.001 — Brute Force: Password Guessing
This applies because repeated failed login attempts were generated against the Windows system.

## T1021.001 — Remote Services: Remote Desktop Protocol
This applies because the attack path used RDP to access the target Windows machine.

## T1078 — Valid Accounts
This applies because a successful login occurred after repeated failures, suggesting the attacker may have obtained valid credentials.

## Summary
The observed behavior maps to a classic credential access and remote access scenario:
- password guessing
- remote service abuse
- possible use of valid credentials
