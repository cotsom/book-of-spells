# Powershell

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
