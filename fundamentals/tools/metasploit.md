---
description: Basic Sheet
icon: hand-holding-skull
---

# Metasploit

<mark style="color:purple;">**Search:**</mark>

```bash
search <name>
#Use
use <name>

#See options
options

#Set options
set
```

<mark style="color:purple;">**Sessions**</mark>

```bash
#list active sessions
sessions
#On meterpreter
background

#New payload
use exploit <exploitname>
set session <sessionID>

```

<mark style="color:purple;">**Modules**</mark>

```bash
#Recon
use post/multi/recon
#Muli handler
use exploit/multi/handler
# local exploits
use post/multi/recon/local_exploit_suggester
```

<mark style="color:purple;">**Payloads**</mark>

```bash
#Windows
set payload windows/meterpreter/reverse_tcp
```
