## Suspicious Debugger Backdoor Created
 
```Kusto
DeviceRegistryEvents
| where RegistryKey contains @"\CurrentVersion\Image File Execution Options\"
| where RegistryKey contains "utilman.exe" or RegistryKey contains "osk.exe" or RegistryKey contains "magnify.exe" or RegistryKey contains "narrator.exe" or RegistryKey contains "displayswitch.exe" or RegistryKey contains "atbroker.exe"
```