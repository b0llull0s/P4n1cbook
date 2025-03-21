---
description: Telecomunications Network - Port 23
icon: tty-answer
---

# Telnet

<details>

<summary><mark style="color:purple;"><strong><code>Commands</code></strong></mark></summary>

{% code title="Escape Characters" %}
```
CTRL + ]
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>IMAP - Internet Message Access Protocol</code></strong></mark></summary>

* <mark style="color:purple;">Uses</mark> <mark style="color:orange;">**`Port 143`**</mark> <mark style="color:purple;">by default.</mark>

<kbd><mark style="color:orange;">**`Custom Client PoC`**<mark style="color:orange;"></kbd>

{% code title="Connect" %}
```sh
telnet <URL> 143
```
{% endcode %}

{% code title="Login" %}
```bash
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
```
a4 FETCH 1 BODY[]
```
{% endcode %}

</details>
