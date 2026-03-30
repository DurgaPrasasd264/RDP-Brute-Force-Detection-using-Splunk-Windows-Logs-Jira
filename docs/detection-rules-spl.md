
# Detection 1: Failed Login Attempt Threshold


index=windows_security EventCode=4625
| stats count by Source_Network_Address, host, Account_Name
| where count >= 5



# Detection 2: RDP Brute Force Detection


index=windows_security EventCode=4625 Logon_Type=10
| stats count by Source_Network_Address, host, Account_Name
| where count >= 5



# Detection 3: Successful Login Occur


index=windows_security EventCode=4624
| stats count by Source_Network_Address, host, Account_Name



# Detection 4: Successful Login After Failures


index=windows_security (EventCode=4624 OR EventCode=4625)
| stats count(eval(EventCode=4625)) as failed_attempts
        count(eval(EventCode=4624)) as successful_logins
  by Source_Network_Address, host, Account_Name
| where failed_attempts >= 5 AND successful_logins > 0
