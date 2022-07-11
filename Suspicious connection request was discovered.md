## Suspicious connection request was discovered
 
```Kusto
let domains_LOTS = (externaldata(LOTS_domain: string)
[@"https://pastebin.com/raw/9gVhAPAb"]
with (format="txt"))
| project LOTS_domain;
domains_LOTS
| join (DeviceNetworkEvents
| where Timestamp > ago(1d)
) on $left.LOTS_domain == $right.RemoteUrl
| where InitiatingProcessVersionInfoOriginalFileName == "curl.exe" or InitiatingProcessCommandLine == "powershell.exe"
| where LOTS_domain contains RemoteUrl
```