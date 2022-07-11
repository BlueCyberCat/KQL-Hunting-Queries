## Microsoft Office Product Spawning Windows Shell
 
```Kusto
DeviceProcessEvents 
| where (((InitiatingProcessFolderPath endswith @"\WINWORD.EXE" or InitiatingProcessFolderPath endswith @"\EXCEL.EXE" or InitiatingProcessFolderPath endswith @"\POWERPNT.exe" or InitiatingProcessFolderPath endswith @"\MSPUB.exe" or InitiatingProcessFolderPath endswith @"\OUTLOOK.EXE" or InitiatingProcessFolderPath endswith @"\EQNEDT32.EXE") and (FolderPath endswith @"\cmd.exe" or FolderPath endswith @"\powershell.exe" or FolderPath endswith @"\wscript.exe" or FolderPath endswith @"\cscript.exe" or FolderPath endswith @"\sh.exe" or FolderPath endswith @"\bash.exe" or FolderPath endswith @"\scrcons.exe" or FolderPath endswith @"\schtasks.exe" or FolderPath endswith @"\regsvr32.exe" or FolderPath endswith @"\hh.exe" or FolderPath endswith @"\wmic.exe" or FolderPath endswith @"\mshta.exe" or FolderPath endswith @"\rundll32.exe" or FolderPath endswith @"\msiexec.exe" or FolderPath endswith @"\forfiles.exe" or FolderPath endswith @"\scriptrunner.exe" or FolderPath endswith @"\mftrace.exe" or FolderPath endswith @"\AppVLP.exe" or FolderPath endswith @"\svchost.exe" or FolderPath endswith @"\msbuild.exe")) and not ((InitiatingProcessFolderPath endswith @"\OUTLOOK.EXE" and FolderPath endswith @"\rundll32.exe" and ProcessCommandLine contains @"\PhotoViewer.dll")) )
// False positives
| where (ProcessCommandLine !contains "msiexec.exe /X" and ProcessCommandLine !contains "/QB") //MSI execution
| where ProcessCommandLine != @"cmd.exe /c ping 192.168.90.100 -n 1 | clip"
| where ProcessCommandLine !startswith @"rundll32.exe cryptext.dll,CryptExtAddPFX C:\"
```