---
icon: golang
description: Directory and file brute-forcing, as well as DNS and virtual host enumeration
---

# Gobuster

{% hint style="info" %}
## <mark style="color:purple;">Engine Options</mark>

* <mark style="color:orange;">**`-u`**</mark> <mark style="color:purple;">-> URL or domain to target.</mark>
* <mark style="color:orange;">**`-w`**</mark> <mark style="color:purple;">-> Wordlist file for brute-forcing.</mark>
* <mark style="color:orange;">**`-t`**</mark> <mark style="color:purple;">-> Number of threads for concurrent requests.</mark>
* <mark style="color:orange;">**`-s`**</mark> <mark style="color:purple;">-> HTTP status codes to include (e.g., 200, 301).</mark>
* <mark style="color:orange;">**`-b`**</mark> <mark style="color:purple;">-> Exclude status codes.</mark>
* <mark style="color:orange;">**`-o`**</mark> <mark style="color:purple;">-> Output file to save results.</mark>
* <mark style="color:orange;">**`-x`**</mark> <mark style="color:purple;">-> File extensions to append to each word in the list (e.g., .php)</mark>
* <mark style="color:orange;">**`-l`**</mark> <mark style="color:purple;">-> Follow redirects (useful for testing against web apps)</mark>
* <mark style="color:orange;">**`-a`**</mark> <mark style="color:purple;">-> Set a custom user-agent.</mark>
* <mark style="color:orange;">**`-c`**</mark> <mark style="color:purple;">-> Custom headers to include in requests.</mark>
* <mark style="color:orange;">**`-k`**</mark> <mark style="color:purple;">-> Ignore SSL certificate verification errors.</mark>
* <mark style="color:orange;">**`-z`**</mark> <mark style="color:purple;">-> Set timeout for each request.</mark>
{% endhint %}

{% hint style="info" %}
## <mark style="color:purple;">Directory Scanning</mark>

{% code title="Basic Scan" %}
```bash
gobuster dir -u http://IP -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
```
{% endcode %}

{% code title="Stealthy Scan" %}
```bash
gobuster dir -u http://example.com -w /path/to/wordlist.txt -t 2 -z 20s -a "Mozilla/5.0" -q -c "X-Forwarded-For: 192.168.1.100"
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">File Scanning</mark>

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
## <mark style="color:purple;">Sub-Domain Scanning</mark>

{% code title="Enumerate Virtual Host" %}
```bash
gobuster vhost -u http://IP -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -t 200
```
{% endcode %}

{% code title="DNS " %}
```bash
gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt
```
{% endcode %}

{% code title="Show IPs of discovered subdomains" %}
```bash
gobuster dns -d example.com -w subdomains.txt -i
```
{% endcode %}

{% code title="DNS Reverse Lookup" %}
```bash
gobuster dns -d example.com -w /path/to/wordlist.txt -r -t 50
```
{% endcode %}
{% endhint %}

***

