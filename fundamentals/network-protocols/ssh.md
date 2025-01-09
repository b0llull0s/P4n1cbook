---
icon: key
description: Secure Shell Protocol
---

# SSH

{% hint style="info" %}
#### <mark style="color:orange;">`Port 22`</mark>
{% endhint %}

***

## <mark style="color:purple;">Key generation</mark>

{% tabs %}
{% tab title="RSA" %}
```sh
ssh-keygen -b 4096
```
{% endtab %}

{% tab title="Ed25519" %}
```sh
ssh-keygen -t ed25519
```
{% endtab %}

{% tab title="ECDSA" %}
```sh
ssh-keygen -t ecdsa-sk
```
{% endtab %}

{% tab title="FIDO/U2F" %}
```sh
ssh-keygen -t ed25519-sk
```

{% hint style="info" %}
{% code title="No-Touch Mode" %}
```sh
ssh-keygen -O no-touch-required -t ed25519-sk
```
{% endcode %}

{% code title="Allow mode on sshd" %}
```sh
no-touch-required sk-ssh-ed25519@openssh.com AAAAInN... user@example.com
```
{% endcode %}
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
{% code title="Details" %}
```sh
ssh-keygen -C "$(whoami)@$(uname -n)-$(date -I)"
```
{% endcode %}

{% code title="Key lenght" %}
```sh
ssh-keygen -l -f public_key
```
{% endcode %}
{% endhint %}

## <mark style="color:purple;">Trouble Shooting</mark>

{% hint style="warning" %}
{% code title="SSH2_MSG_KEX_ECDH_REPLY" fullWidth="true" %}
```sh
ssh -o MACs=hmac-sha2-256 <HOST>
```
{% endcode %}

***

* <mark style="color:purple;">Sometimes the</mark> <mark style="color:orange;">**`/etc/hosts.allow`**</mark> <mark style="color:purple;">or</mark> <mark style="color:orange;">**`/etc/hosts.deny`**</mark> <mark style="color:purple;">may be configured to blacklist or whitelist IPs trying to connect to the server:</mark>

{% code title="Whitelist an IP" %}
```
ALL : 10.10.16.8

```
{% endcode %}

* <mark style="color:purple;">Add that in the</mark> <mark style="color:orange;">**`/hosts.allow`**</mark> <mark style="color:purple;">file; make sure to let a blank line at the end.</mark>
* <mark style="color:orange;">**`sshd_wl`**</mark> <mark style="color:purple;">is the syslink to</mark> <mark style="color:orange;">**`host.allow`**</mark> <mark style="color:purple;">and is normally in</mark> <mark style="color:orange;">**`.ssh`**</mark>

***

* <mark style="color:purple;">In recent versions of</mark> <mark style="color:orange;">**`OpenSSH`**</mark><mark style="color:purple;">, certain older key types like</mark> <mark style="color:orange;">**`ssh-rsa`**</mark> <mark style="color:purple;">have been deprecated because of security concerns with the</mark> <mark style="color:orange;">**`SHA-1`**</mark> <mark style="color:purple;">hash algorithm they use:</mark>

```sh
ssh root@10.10.10.34 -i id_rsa -o PubkeyAcceptedKeyTypes=ssh-rsa
```
{% endhint %}

## <mark style="color:purple;">**OpenSSH Vulnerabilities**</mark>

{% embed url="https://repology.org/project/openssh/cves?version=8.9.p1" %}

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

***

{% hint style="danger" %}
### <mark style="color:orange;">`CVE-2008-0166`</mark>

* <mark style="color:orange;">**`Debian OpenSSL Predictable PRNG`**</mark> <mark style="color:purple;">-> Check the</mark> [<mark style="color:purple;">**repo**</mark>](https://github.com/g0tmi1k/debian-ssh/tree/master)
* <mark style="color:purple;">Look for matches for a given</mark> <mark style="color:orange;">**`public_key`**</mark><mark style="color:purple;">:</mark>

```sh
grep -R -n `cat public_key` rsa/
```
{% endhint %}
