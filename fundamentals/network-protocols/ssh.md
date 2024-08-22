---
icon: key
description: Secure Shell Protocol
---

# SSH

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

# No-Touch Mode
ssh-keygen -O no-touch-required -t ed25519-sk
# Allow touch mode on sshd
no-touch-required sk-ssh-ed25519@openssh.com AAAAInN... user@example.com
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
{% code title="Details" %}
```sh
ssh-keygen -C "$(whoami)@$(uname -n)-$(date -I)"
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
{% endhint %}

## <mark style="color:purple;">**OpenSSH Vulnerabilities**</mark>

{% embed url="https://repology.org/project/openssh/cves?version=8.9.p1" %}
