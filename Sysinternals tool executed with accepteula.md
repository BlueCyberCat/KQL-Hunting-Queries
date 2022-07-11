## Sysinternals tool executed with accepteula
 
```Kusto
DeviceProcessEvents 
| where ProcessVersionInfoCompanyName == @"Sysinternals - www.sysinternals.com"
| where ProcessCommandLine contains "accepteula"
```