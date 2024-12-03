---
icon: golang
description: Directory and file brute-forcing, as well as DNS and virtual host enumeration
---

# Gobuster

{% hint style="info" %}
## <mark style="color:purple;">Global Options</mark>

* <mark style="color:orange;">**`-u`**</mark> <mark style="color:purple;">-> URL or domain to target.</mark>
* <mark style="color:orange;">**`-w`**</mark> <mark style="color:purple;">-> Wordlist file for brute-forcing.</mark>
* <mark style="color:orange;">**`-t`**</mark> <mark style="color:purple;">-> Number of threads for concurrent requests.</mark>
* <mark style="color:orange;">**`-q`**</mark> <mark style="color:purple;">-> Quiet mode.</mark>
* <mark style="color:orange;">**`-i`**</mark> <mark style="color:purple;">-> Show IP addresses.</mark>
* <mark style="color:orange;">**`-o`**</mark> <mark style="color:purple;">-> Output file to save results.</mark>
* <mark style="color:orange;">**`-v`**</mark> <mark style="color:purple;">-> Verbose mode.</mark>
* <mark style="color:orange;">**`-z`**</mark> <mark style="color:purple;">-> Don't display progress.</mark>
* <mark style="color:orange;">**`--delay duration`**</mark> <mark style="color:purple;">-></mark> <mark style="color:orange;">**`DNS`**</mark> <mark style="color:purple;">resolver output.</mark>
{% endhint %}

{% hint style="info" %}
## <mark style="color:purple;">Directory Scanning</mark>

{% code title="Basic Scan" %}
```bash
gobuster dir -u http://IP -w /directory-list-2.3-medium.txt
```
{% endcode %}

{% code title="Show length" %}
```sh
gobuster dir -u https://example.com -w ~/wordlists/shortlist.txt -l
```
{% endcode %}

{% code title="Stealthy Scan" overflow="wrap" %}
```bash
gobuster dir -u http://example.com -w /path/to/wordlist.txt -t 2 -z 20s -a "Mozilla/5.0" -q -c "X-Forwarded-For: 192.168.1.100"
```
{% endcode %}

***

### <mark style="color:purple;">Options</mark>

* <mark style="color:orange;">**`-h`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Manual.</mark>&#x20;
* <mark style="color:orange;">**`-f`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Append</mark> <mark style="color:orange;">**`/`**</mark> <mark style="color:purple;">to each request.</mark>
* <mark style="color:orange;">**`-c`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Provide Cookie.</mark>
* <mark style="color:orange;">**`-e`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Expanded mode.</mark>
* <mark style="color:orange;">**`-x`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;">Search for file extensions.</mark>
* <mark style="color:orange;">**`-r`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Follow redirects.</mark>
* <mark style="color:orange;">**`-H`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;">Specify</mark> <mark style="color:orange;">**`HTTP`**</mark> <mark style="color:purple;">headers.</mark>
* <mark style="color:orange;">**`-I`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark> <mark style="color:purple;"></mark><mark style="color:purple;">Include length.</mark>
* <mark style="color:orange;">**`-k`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Skip</mark> <mark style="color:orange;">**`TLS`**</mark> <mark style="color:purple;">certificate verification.</mark>
* <mark style="color:orange;">**`-n`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Don't print status codes.</mark>
* <mark style="color:orange;">**`-U`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">User name for</mark> <mark style="color:orange;">**`Basic Auth`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:orange;">**`-P`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Password for</mark> <mark style="color:orange;">**`Basic Auth`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:orange;">**`-p`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Provide a proxy.</mark>
* <mark style="color:orange;">**`-s`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Print Status code.</mark>
* <mark style="color:orange;">**`-b`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Print blacklisted status codes.</mark>
* <mark style="color:orange;">**`--timeout duration`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:orange;">**`HTTP`**</mark> <mark style="color:purple;">Timeout.</mark>
* <mark style="color:orange;">**`-u`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Target</mark> <mark style="color:orange;">**`URL`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:orange;">**`-a`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Set</mark> <mark style="color:orange;">**`User-agent`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:orange;">**`-d`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Search for backup files once a file is discovered.</mark>
* <mark style="color:orange;">**`--wildcard`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">continue scanning</mark> <mark style="color:purple;"></mark><mark style="color:purple;">**even if a wildcard**</mark>**&#x20;**<mark style="color:orange;">**`DNS`**</mark> <mark style="color:purple;">entry or a similar issue is detected.</mark>
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">File Scanning</mark>

{% code title="Bunch of files" overflow="wrap" %}
```bash
gobuster dir -u http://IP -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 150 -x .php,.html,.py,.git,.sh,.bak,.js,.txt,.git
```
{% endcode %}

{% code title="Txt files" overflow="wrap" %}
```bash
gobuster dir -u http://10.10.10.60 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .txt -t 40
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">Sub-Domain Scanning</mark>

### <mark style="color:orange;">`VHOST`</mark>

{% code title="Enumerate Virtual Host" overflow="wrap" %}
```bash
gobuster vhost -u http://IP -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -t 200
```
{% endcode %}

***

### <mark style="color:orange;">`DNS`</mark>

{% code title="Standard Scan " overflow="wrap" %}
```bash
gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt
```
{% endcode %}

{% code title="Show IP" %}
```bash
gobuster dns -d example.com -w subdomains.txt -i
```
{% endcode %}

{% code title="DNS Reverse Lookup" %}
```bash
gobuster dns -d example.com -w /path/to/wordlist.txt -r -t 50
```
{% endcode %}

### <mark style="color:purple;">Options</mark>

* <mark style="color:orange;">**`-h`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Manual.</mark>
* <mark style="color:orange;">**`-c`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Provide Cookie.</mark>
* <mark style="color:orange;">**`-r`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Follow redirects.</mark>
* <mark style="color:orange;">**`-H`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;">Specify</mark> <mark style="color:orange;">**`HTTP`**</mark> <mark style="color:purple;">headers.</mark>
* <mark style="color:orange;">**`-k`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Skip</mark> <mark style="color:orange;">**`TLS`**</mark> <mark style="color:purple;">certificate verification.</mark>
* <mark style="color:orange;">**`-U`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">User name for</mark> <mark style="color:orange;">**`Basic Auth`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:orange;">**`-P`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Password for</mark> <mark style="color:orange;">**`Basic Auth`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:orange;">**`-p`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Provide a proxy.</mark>
* <mark style="color:orange;">**`--timeout duration`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:orange;">**`HTTP`**</mark> <mark style="color:purple;">Timeout.</mark>
* <mark style="color:orange;">**`-u`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Target</mark> <mark style="color:orange;">**`URL`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:orange;">**`-a`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Set</mark> <mark style="color:orange;">**`User-agent`**</mark><mark style="color:purple;">.</mark>
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:orange;">`S3`</mark> <mark style="color:purple;">Scanning</mark>

{% code title="Scan Buckets" %}
```sh
gobuster s3 -w bucket-names.txt
```
{% endcode %}
{% endhint %}

