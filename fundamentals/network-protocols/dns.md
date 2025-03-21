---
description: Domain Name System - Port 53
icon: building-memo
---

# DNS

<details>

<summary><mark style="color:purple;"><strong><code>Enumeration</code></strong></mark></summary>

{% hint style="info" %}


#### <mark style="color:red;">`Resolve the IP`</mark>

{% code title="Start nslookup" %}
```sh
nslookup
```
{% endcode %}

* <mark style="color:purple;">Specify the</mark> <mark style="color:orange;">**`DNS`**</mark> <mark style="color:purple;">server:</mark>

```sh
server 10.10.10.10
```

* <mark style="color:purple;">Now, query for the given IP address, looking up its</mark> <mark style="color:orange;">**`DNS`**</mark> <mark style="color:purple;">records:</mark>

```
10.10.10.10
```
{% endhint %}

{% hint style="info" %}


#### <mark style="color:red;">**`Transfer Zones`**</mark>

* <mark style="color:purple;">If</mark> <mark style="color:orange;">`DNS`</mark> <mark style="color:purple;">is running over</mark> <mark style="color:orange;">`TCP`</mark> <mark style="color:purple;">try a zone transfer:</mark>

```sh
dig axfr HOST.NAME @10.10.10.29
```
{% endhint %}

</details>
