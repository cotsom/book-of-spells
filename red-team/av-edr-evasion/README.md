# AV / EDR Evasion

Get info about antimalware on system

```
powershell Get-MpPreference | fl @{n='ExclusionProcess'; e={$_.ExclusionProcess|Out-String}}, @{n='ExclusionPath'; e={$_.ExclusionPath|Out-String}}, @{n='ExclusionExtension'; e={$_.ExclusionExtension|Out-String}}, @{n='ExclusionIpAddress'; e={$_.ExclusionIpAddress|Out-String}}, DisableRealtimeMonitoring, DisableBehaviorMonitoring, DisableEmailScanning, DisableIOAVProtection, DisableScriptScanning
```
