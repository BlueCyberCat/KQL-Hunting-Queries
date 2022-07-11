## Executing of Bloodhound AD reconnaissance tool
 
```Kusto
DeviceProcessEvents 
| where ProcessVersionInfoOriginalFileName == @"BloodHound.exe" or ProcessVersionInfoCompanyName contains "Vazarkar"
```