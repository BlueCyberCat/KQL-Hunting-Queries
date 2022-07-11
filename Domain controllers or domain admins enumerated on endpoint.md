## Domain controllers or domain admins enumerated on endpoint
 
```Kusto
DeviceProcessEvents
| where FileName == "net.exe" or FileName == "net1.exe"
| where InitiatingProcessCommandLine contains "domain controllers" or InitiatingProcessCommandLine contains "domain admins"
```