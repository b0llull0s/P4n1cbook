---
description: Internet Printing Protocol
icon: print
---

# IPP

{% hint style="info" %}
### <mark style="color:orange;">`CUPS`</mark> <mark style="color:purple;">(Common UNIX Printing System)</mark>

* <mark style="color:purple;">It uses</mark> <mark style="color:orange;">**`UDP`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`TCP`**</mark> <mark style="color:purple;">**on Port**</mark> <mark style="color:orange;">**`631`**</mark>

### <mark style="color:purple;">Vulnerabilities</mark>

[<mark style="color:red;">**`CVE-2024-47176`**</mark>](https://nvd.nist.gov/vuln/detail/CVE-2024-47176)

* <mark style="color:orange;">**`cups-browsed`**</mark><mark style="color:purple;">, the service that typically listens on all interfaces</mark> <mark style="color:orange;">**`UDP 631`**</mark><mark style="color:purple;">, is what allows adding a printer to a machine remotely. This vulnerability allows any attacker who can reach this machine to trigger a</mark> <mark style="color:orange;">**`“Get-Printer-Attributes” IPP`**</mark> <mark style="color:purple;">request being sent to an attacker-controlled URL.</mark>

[<mark style="color:red;">**`CVE-2024-47076`**</mark>](https://nvd.nist.gov/vuln/detail/CVE-2024-47076)

* <mark style="color:orange;">**`libcupsfilters`**</mark> <mark style="color:purple;">is responsible for handling the</mark> <mark style="color:orange;">**`IPP`**</mark> <mark style="color:purple;">attributes returned from the request. These are written to a temporary</mark> <mark style="color:orange;">**`Postscript Printer Description (PPD)`**</mark> <mark style="color:purple;">file without sanitization, allowing malicious attributes to be written.</mark>

[<mark style="color:red;">**`CVE-2024-47175`**</mark>](https://nvd.nist.gov/vuln/detail/CVE-2024-47175)

* <mark style="color:orange;">**`libppd`**</mark> <mark style="color:purple;">is responsible for reading a temporary</mark> <mark style="color:orange;">**`PPD`**</mark> <mark style="color:purple;">file and turning that into a printer object on the system. It also doesn’t sanitize when reading, allowing for injection of attacker controlled data.</mark>

[<mark style="color:red;">**`CVE-2024-47177`**</mark>](https://nvd.nist.gov/vuln/detail/CVE-2024-47177)

* <mark style="color:purple;">This vulnerability in</mark> <mark style="color:orange;">**`cups-filters`**</mark> <mark style="color:purple;">allows for loading a printer using the</mark> <mark style="color:orange;">**`foomatic-rip`**</mark> <mark style="color:purple;">print filter, which is a universal converter for transforming PostScript or PDF data into the format that the printer can understand. It has long had issues with command injection, and has been limited to manual installs / configurations only.</mark>

### <mark style="color:orange;">`POC`</mark>

* <mark style="color:purple;">Ippsec has a</mark> [<mark style="color:orange;">**`POC`**</mark>](https://github.com/ippsec/evil-cups) <mark style="color:purple;">that is used on the evilcups machine from HackThebox</mark>
{% endhint %}
