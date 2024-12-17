---
icon: building-memo
description: Domain Name System
---

# DNS

{% hint style="info" %}
### <mark style="color:purple;">Enumeration</mark>

#### <mark style="color:purple;">Resolve the IP:</mark>

{% code title="Start the tool" %}
```bash
nslookup
```
{% endcode %}

* <mark style="color:purple;">Specify the</mark> <mark style="color:orange;">**`DNS`**</mark> <mark style="color:purple;">server:</mark>

```
server 10.10.10.10
```

* <mark style="color:purple;">Now, query for the given IP address, looking up its</mark> <mark style="color:orange;">**`DNS`**</mark> <mark style="color:purple;">records:</mark>

```
10.10.10.10
```

***

#### <mark style="color:purple;">If</mark>  <mark style="color:orange;">`DNS`</mark> <mark style="color:purple;">is running over</mark> <mark style="color:orange;">`TCP`</mark> <mark style="color:purple;">try a zone transfer:</mark>&#x20;

```bash
dig axfr HOST.NAME @10.10.10.29
```
{% endhint %}



