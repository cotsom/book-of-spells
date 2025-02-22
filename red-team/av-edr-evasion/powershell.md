# Powershell

### Obfuscate scripts

[**SecureSting**](https://www.wietzebeukema.nl/blog/powershell-obfuscation-using-securestring)

[**ObfuctationBible**](https://github.com/t3l3machus/PowerShell-Obfuscation-Bible)

### Constrained Language Mode Bypass

Research [Source](https://pentestn00b.wordpress.com/2017/03/20/simple-bypass-for-powershell-constrained-language-mode/)&#x20;

```powershell
powershell.exe -version 2
```

### Check groups & SID with WMI

```powershell
# determine current user
$currentUser = [System.Security.Principal.WindowsIdentity]::GetCurrent()

# Get list of security tokens
$privileges = @()
$currentUser.Groups | ForEach-Object {
    $group = $_
    $sid = $group.Value
    $priv = New-Object -TypeName PSObject -Property @{
        SID = $sid
        Name = (New-Object System.Security.Principal.SecurityIdentifier($sid)).Translate([System.Security.Principal.NTAccount]).Value
    }
    $privileges += $priv
}

# output groups list
$privileges | Format-Table
```
