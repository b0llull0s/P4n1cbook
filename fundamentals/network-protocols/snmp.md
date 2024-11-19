---
icon: shredder
description: Simple Network Management Protocol
---

# SNMP

{% hint style="warning" %}
<mark style="color:purple;">**Uses**</mark> <mark style="color:orange;">**`UDP`**</mark>
{% endhint %}

{% tabs %}
{% tab title="Port 161" %}
* <mark style="color:purple;">**Used for sending**</mark>** **<mark style="color:orange;">**`SNMP`**</mark> <mark style="color:purple;">**requests to network devices.**</mark>
{% endtab %}

{% tab title="Port 162" %}
* <mark style="color:purple;">**Used for receiving**</mark>** **<mark style="color:orange;">**`SNMP`**</mark>** **<mark style="color:purple;">**notifications (**</mark><mark style="color:orange;">**`Traps`**</mark>** **<mark style="color:purple;">**and**</mark>** **<mark style="color:orange;">**`InformRequests`**</mark><mark style="color:purple;">**) from network devices.**</mark>
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
* ## <mark style="color:purple;">Install</mark> <mark style="color:orange;">`MIBs`</mark>

{% code title="Arch" %}
```sh
sudo pacman -Sy snmp-mibs-downloader
```
{% endcode %}

{% code title="Kali" %}
```sh
sudo apt install snmp-mibs-downloader
```
{% endcode %}

* ## <mark style="color:purple;">Install</mark> <mark style="color:orange;">`snmpwalk`</mark>

{% code title="Arch" %}
```sh
// Some code
```
{% endcode %}

{% code title="Kali" %}
```sh
// Some code
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">Enumeration</mark>

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

