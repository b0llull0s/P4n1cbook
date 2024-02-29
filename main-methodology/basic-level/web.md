---
description: Enumeration and Bruteforcing
---

# 🕸️ Web

**Curl:**

```bash
curl -k -v <IP>
#2
curl -s -k -v -i <ip>
```

#### Nmap:

```
nmap --script http-enum -p80 <IP>
#Scan Path:
nmap -n -p80 --script http-enum --script-args http-enum.basepath='/<PATH>' <IP>
```

#### Brute-Forcing

feroxbuster:

```
feroxbuster -u
```
