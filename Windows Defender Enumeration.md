## Windows Defender Enumeration
 
```Kusto
DeviceEvents 
| project-away FileName, FolderPath, SHA1, SHA256, MD5, FileSize, AccountDomain, AccountName, AccountSid, RemoteUrl, RemoteDeviceName, ProcessId, ProcessCommandLine, ProcessCreationTime, ProcessTokenElevation, LogonId, RegistryKey, RegistryValueName, RegistryValueData, RemoteIP, RemotePort, LocalIP,LocalPort, FileOriginIP, FileOriginUrl
| where AdditionalFields contains "Get-MpPreference"
| where InitiatingProcessFileName != ""
| where InitiatingProcessParentFileName != @"idea64.exe"
| where InitiatingProcessParentFileName != @"SenseIR.exe"
| where InitiatingProcessParentFileName != @"rider64.exe"
| where InitiatingProcessParentFileName != @"webstorm64.exe"
| where InitiatingProcessParentFileName != @"pycharm64.exe"
| where InitiatingProcessParentFileName != @"datagrip64.exe"
| join kind=leftouter (DeviceLogonEvents
| project Timestamp, DeviceName,ActionType, LogonType,AccountName, Protocol,RemoteIP, AdditionalFields, LogonId) 
on $left.InitiatingProcessLogonId == $right.LogonId
```