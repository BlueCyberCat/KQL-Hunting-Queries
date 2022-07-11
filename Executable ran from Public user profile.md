## Executable ran from Public user profile
 
```Kusto
DeviceProcessEvents 
| where FolderPath contains @"C:\Users\Public"
```
