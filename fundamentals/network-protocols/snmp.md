---
description: Simple Network Management Protocol - Port 161/162
icon: shredder
---

# SNMP

{% hint style="info" %}
* <mark style="color:purple;">**Uses**</mark> <mark style="color:orange;">**`UDP`**</mark>
* <mark style="color:orange;">**`Port 161`**</mark> <mark style="color:purple;">**for sending**</mark>**&#x20;**<mark style="color:orange;">**`SNMP`**</mark> <mark style="color:purple;">**requests.**</mark>
* <mark style="color:orange;">**`Port 162`**</mark> <mark style="color:purple;">**for receiving**</mark>**&#x20;**<mark style="color:orange;">**`SNMP`**</mark>**&#x20;**<mark style="color:purple;">**notifications (**</mark><mark style="color:orange;">**`Traps`**</mark>**&#x20;**<mark style="color:purple;">**and**</mark>**&#x20;**<mark style="color:orange;">**`InformRequests`**</mark><mark style="color:purple;">**)**</mark>
{% endhint %}

<details>

<summary><mark style="color:orange;"><strong><code>MIBs</code></strong></mark></summary>

{% code title="Installation" %}
```bash
sudo pacman -Sy snmp-mibs-downloader
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Enumeration</code></strong></mark></summary>

{% code title="SNMP System Description" overflow="wrap" %}
```sh
nmap -sU -p 161 -script snmp-sysdescr -script-args snmpcommunity=admin 192.168.1.1
```
{% endcode %}

{% code title="Install snmpwalk" %}
```sh
sudo pacman -Sy net-snmp
```
{% endcode %}

{% code title="Install onesixtyone" %}
```bash
yay -S onesixtyone-git 
```
{% endcode %}

{% hint style="info" %}
{% code title="Full Enumeration" %}
```bash
snmpwalk -v 2c -c public 10.10.10.92
```
{% endcode %}

{% code title="Scan SNMP on an IP" %}
```bash
snmpwalk -v 2c -c public 10.129.42.253 1.3.6.1.2.1.1.5.0
```
{% endcode %}

{% code title="Enumerate Process" %}
```bash
snmpbulkwalk -v2c -c public 10.10.10.92 hrSWRunName
```
{% endcode %}

{% code title="Enumerate within processes" %}
```bash
snmpbulkwalk -v2c -c public 10.10.10.92 hrSWRunTable | grep <PID>
```
{% endcode %}

{% code title="Enumerate Interfaces" %}
```bash
snmpbulkwalk -v2c -c public 10.10.10.92 ipAddressType
```
{% endcode %}

{% code title="Brute force Secret String" %}
```bash
onesixtyone -c dict.txt 10.129.42.254
```
{% endcode %}
{% endhint %}

</details>
