# AV / EDR Evasion

Get info about antimalware on system

```powershell
powershell Get-MpPreference | fl @{n='ExclusionProcess'; e={$_.ExclusionProcess|Out-String}}, @{n='ExclusionPath'; e={$_.ExclusionPath|Out-String}}, @{n='ExclusionExtension'; e={$_.ExclusionExtension|Out-String}}, @{n='ExclusionIpAddress'; e={$_.ExclusionIpAddress|Out-String}}, DisableRealtimeMonitoring, DisableBehaviorMonitoring, DisableEmailScanning, DisableIOAVProtection, DisableScriptScanning
```

Get info about av excludes without rights

```powershell
Get-WinEvent -LogName "Microsoft-Windows-Windows Defender/Operational" -FilterXPath "*[System[(EventID=5007)]]" | Where-Object { $_.Message -like  "*exclusions\Path*" } | Select-Object  Message | FL
```
