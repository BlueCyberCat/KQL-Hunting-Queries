## Suspicious Discord connection was observed
 
```Kusto
union DeviceNetworkEvents, DeviceProcessEvents 
| where RemoteUrl == "https://discord.com" or ProcessCommandLine contains "discord.com/api/webhooks"
| where InitiatingProcessVersionInfoOriginalFileName == "curl.exe" or ProcessVersionInfoOriginalFileName == "curl.exe" or InitiatingProcessCommandLine == "powershell.exe"
| sort by Timestamp desc  
```