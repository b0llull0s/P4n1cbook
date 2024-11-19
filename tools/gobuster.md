---
icon: golang
---

# Gobuster

{% hint style="info" %}
## Directory Scanning

{% code title="Basic Scan" %}
```bash
gobuster dir -u http://IP -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
```
{% endcode %}

{% code title="Self-signed Certificate" %}
```bash
gobuster dir -u https://beep.htb -w /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt -k
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## File Scanning

{% code title="Bunch of files" %}
```bash
gobuster dir -u http://IP -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 150 -x .php,.html,.py,.git,.sh,.bak,.js,.txt,.git
```
{% endcode %}

{% code title="Txt files" %}
```bash
gobuster dir -u http://10.10.10.60 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .txt -t 40
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## Domain Scanning

{% code title="top1million" %}
```bash
gobuster vhost -u http://IP -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -t 200
```
{% endcode %}


{% endhint %}

