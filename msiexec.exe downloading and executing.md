## msiexec.exe downloading and executing packages
 
```Kusto
DeviceProcessEvents 
| where ProcessVersionInfoInternalFileName == @"msiexec"
| where ProcessCommandLine contains "http"
| where (ProcessCommandLine contains "/q" or ProcessCommandLine contains "-q")
```