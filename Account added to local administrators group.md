## Account added to local administrators group
 
```Kusto
DeviceProcessEvents 
| where FileName == "net.exe" or FileName == "net1.exe"
| where ProcessCommandLine has "/add" and ProcessCommandLine has "localgroup"and ProcessCommandLine contains "admin"
| where ProcessCommandLine !contains "ora_dba"
//Open VPN exclusion
| where ProcessCommandLine !contains "OpenVPN Administrators"
| join kind=leftouter (DeviceLogonEvents
| project Timestamp, DeviceName,ActionType, LogonType,AccountName, Protocol,RemoteIP, AdditionalFields, LogonId) 
on $left.LogonId == $right.LogonId
```