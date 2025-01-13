---
icon: tty-answer
---

# Telnet

{% hint style="info" %}
#### <mark style="color:orange;">`Port 23`</mark>

#### <mark style="color:purple;">Basic text-based communication protocol that allows you to interact with remote servers or services</mark>

* <mark style="color:orange;">**`CTRL + ]`**</mark> <mark style="color:purple;">to escape characters.</mark>
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:red;">`IMAP`</mark>

#### <mark style="color:orange;">`Internet Message Access Protocol`</mark>&#x20;

* <mark style="color:purple;">Uses</mark> <mark style="color:orange;">**`Port 143`**</mark> <mark style="color:purple;">by default.</mark>

```sh
telnet <URL> 143
```

{% code title="Login" %}
```sh
a1 LOGIN <Username> <Password>
```
{% endcode %}

{% code title="List all" %}
```sh
a2 LIST "" "*"
```
{% endcode %}

{% code title="Select Mailbox" %}
```sh
a3 EXAMINE INBOX
```
{% endcode %}

{% code title="Fetch the first message" %}
```sh
a4 FETCH 1 BODY[]
```
{% endcode %}
{% endhint %}

