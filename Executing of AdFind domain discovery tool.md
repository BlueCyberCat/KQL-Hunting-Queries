## Executing of AdFind domain discovery tool
 
```Kusto
DeviceProcessEvents 
| where ProcessVersionInfoOriginalFileName == @"AdFind.exe" or ProcessCommandLine contains "adfind"
```