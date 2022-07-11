## Powershell downgrade to version 2
 
```Kusto
DeviceProcessEvents
| where ProcessCommandLine has "powershell"
| where ProcessCommandLine has "-version 2"
```