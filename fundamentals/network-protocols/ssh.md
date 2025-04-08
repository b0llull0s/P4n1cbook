---
description: Secure Shell Protocol - Port 22
icon: key
---

# SSH

<details>

<summary><mark style="color:purple;"><strong><code>Key Generation</code></strong></mark></summary>

{% code title="RSA" overflow="wrap" %}
```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
{% endcode %}

{% code title="Ed25519" %}
```sh
ssh-keygen -t ed25519
```
{% endcode %}

{% code title="ECDSA" overflow="wrap" %}
```sh
ssh-keygen -t ecdsa-sk
```
{% endcode %}

{% hint style="info" %}


#### <mark style="color:red;">**`FIDO/U2F`**</mark>

{% code title="Generate the key" %}
```shell
ssh-keygen -t ed25519-sk
```
{% endcode %}

{% code title="Without Touch-Mode" overflow="wrap" %}
```sh
ssh-keygen -O no-touch-required -t ed25519-sk
```
{% endcode %}

{% code title="Allow mode on sshd" overflow="wrap" %}
```bash
no-touch-required sk-ssh-ed25519@openssh.com AAAAInN... user@example.com
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Enumeration</code></strong></mark></summary>

{% code title="Show Details" %}
```bash
ssh-keygen -C "$(whoami)@$(uname -n)-$(date -I)"
```
{% endcode %}

{% code title="Key lenght" %}
```bash
ssh-keygen -l -f public_key
```
{% endcode %}

{% code title="Check SSH access" %}
```sh
netexec ssh <IP> -u <USER> -p 'password'
```
{% endcode %}

{% code title="SSH Brute Force" overflow="wrap" %}
```sh
nmap -n -p22 --script ssh-brute --script-args userdb=usernames.txt,passdb=passwords.txt <IP>
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Trouble-shooting</code></strong></mark></summary>

{% hint style="info" %}
<mark style="color:red;">**`SSH2_MSG_KEX_ECDH_REPLY`**</mark> <mark style="color:purple;">error:</mark>

```sh
ssh -o MACs=hmac-sha2-256 <HOST>
```
{% endhint %}

{% hint style="info" %}
* <mark style="color:purple;">Sometimes the</mark> <mark style="color:orange;">**`/etc/hosts.allow`**</mark> <mark style="color:purple;">or</mark> <mark style="color:orange;">**`/etc/hosts.deny`**</mark> <mark style="color:purple;">may be configured to blacklist or whitelist</mark> <mark style="color:orange;">**`IPs`**</mark> <mark style="color:purple;">trying to connect to the server:</mark>

{% code title="Whitelist" %}
```
ALL : 10.10.16.8

```
{% endcode %}

* <mark style="color:purple;">Add that in the</mark> <mark style="color:orange;">**`/hosts.allow`**</mark> <mark style="color:purple;">file; make sure to let a blank line at the end.</mark>
* <mark style="color:orange;">**`sshd_wl`**</mark> <mark style="color:purple;">is the syslink to</mark> <mark style="color:orange;">**`host.allow`**</mark> <mark style="color:purple;">and is normally in</mark> <mark style="color:orange;">**`.ssh`**</mark>
{% endhint %}

{% hint style="info" %}
* <mark style="color:purple;">In recent versions of</mark> <mark style="color:orange;">**`OpenSSH`**</mark><mark style="color:purple;">, certain older key types like</mark> <mark style="color:orange;">**`ssh-rsa`**</mark> <mark style="color:purple;">have been deprecated because of security concerns with the</mark> <mark style="color:orange;">**`SHA-1`**</mark> <mark style="color:purple;">hash algorithm they use:</mark>

{% code overflow="wrap" %}
```sh
ssh root@10.10.10.34 -i id_rsa -o PubkeyAcceptedKeyTypes=ssh-rsa
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>OpenSSH Vulnerabilities</code></strong></mark></summary>

#### [<kbd><mark style="color:orange;">**`Repology`**<mark style="color:orange;"></kbd>](https://repology.org/project/openssh/cves?version=8.9.p1)

{% hint style="info" %}
### <mark style="color:orange;">`RsaCtfTool`</mark>

* &#x20;[<mark style="color:orange;">**`RSA attack tool`**</mark>](https://github.com/RsaCtfTool/RsaCtfTool/tree/master) <mark style="color:purple;">(mainly for ctf) - retrieve private key from weak public key and/or uncipher data.</mark>
* <mark style="color:purple;">Install</mark> <mark style="color:orange;">**`libmpc-dev`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`libgmp3-dev`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`sagemath`**</mark>
* <mark style="color:purple;">Also recommend to use a virtual environment</mark>

{% code overflow="wrap" %}
```sh
RsaCtfTool/RsaCtfTool.py --publickey decoder.pub --decryptfile pass.crypt
```
{% endcode %}
{% endhint %}

{% hint style="danger" %}
### <mark style="color:orange;">`CVE-2008-0166`</mark>

* <mark style="color:orange;">**`Debian OpenSSL Predictable PRNG`**</mark> <mark style="color:purple;">-> Check the</mark> [<mark style="color:purple;">**repo**</mark>](https://github.com/g0tmi1k/debian-ssh/tree/master)
* <mark style="color:purple;">Look for matches for a given</mark> <mark style="color:orange;">**`public_key`**</mark><mark style="color:purple;">:</mark>

```sh
grep -R -n `cat public_key` rsa/
```
{% endhint %}

</details>

***
