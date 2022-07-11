## Renamed PsExec or Procdump executed
 
```Kusto
DeviceProcessEvents
| where ProcessVersionInfoOriginalFileName == "procdump" or ProcessVersionInfoInternalFileName == "PsExec"
| where FileName != "PsExec.exe" and FileName != "PsExec64.exe" and FileName != "procdump.exe" and FileName != "procdump64.exe"
```