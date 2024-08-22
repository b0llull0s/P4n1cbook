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

{% tab title="Anonymous login" %}
```
ftp <IP>
# Next type
anonymous
```
{% endtab %}
{% endtabs %}

## <mark style="color:purple;">Enumeration</mark>

{% code title="Check root path" %}
```
pwd / dir
```
{% endcode %}
