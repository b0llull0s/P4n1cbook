---
icon: curling-stone
description: Client URL
---

# curl

{% hint style="info" %}
## <mark style="color:purple;">Basic Options</mark>

{% code title="Verbose" %}
```bash
curl -v <IP>
```
{% endcode %}

{% code title="More Verbose" %}
```bash
curl -vvv <IP>
```
{% endcode %}

{% code title="Show Errors" %}
```bash
curl -S https://example.com
```
{% endcode %}

{% code title="Load options from a local file" %}
```bash
curl -K config.txt
```
{% endcode %}

{% code title="Download a page/file" %}
```bash
curl -O https://example.com
```
{% endcode %}

{% code title="Save file with a custom name" %}
```bash
curl https://example.com -o file.txt
```
{% endcode %}

{% code title="Silent Status" %}
```bash
curl -s inlanefreight.com/index.html
```
{% endcode %}
{% endhint %}

***

{% hint style="success" %}
## <mark style="color:purple;">File Uploads</mark>

{% code title="File Upload" %}
```bash
curl -T example.txt https://example.com/upload
```
{% endcode %}

{% code title="File Upload + POST" %}
```bash
curl -T example.txt -X POST https://example.com/upload
```
{% endcode %}

{% code title="File upload + Authentication" %}
```bash
curl -u user:pass -T example.txt https://example.com/upload
```
{% endcode %}

{% code title="File Upload + Token Authentication" %}
```bash
curl -u :YOUR_TOKEN -T example.txt https://example.com/upload
```
{% endcode %}

{% code title="File Upload + Custom Header" %}
```bash
curl -H "Authorization: Bearer YOUR_TOKEN" -T example.txt https://example.com/upload
```
{% endcode %}

{% code title="File Upload + Multiple Custom Headers" %}
```bash
curl -H "Authorization: Bearer YOUR_TOKEN" -H "Content-Type: application/json" -T example.txt https://example.com/upload
```
{% endcode %}

{% code title="Multiple File Uploads" %}
```bash
curl -T file1.txt -T file2.txt https://example.com/upload
```
{% endcode %}

{% code title="File Upload as Form submission" %}
```bash
curl -F "file=@example.txt" https://example.com/upload
```
{% endcode %}

{% code title="File Upload + Additional Query Parameters" %}
```bash
curl -T example.txt "https://example.com/upload?user=alice&timestamp=2024"
```
{% endcode %}

{% code title="File Upload + Redirect" %}
```bash
curl -L -T example.txt https://example.com/upload
```
{% endcode %}

{% code title="File Upload + Retry" %}
```bash
curl --retry 5 -T example.txt https://example.com/upload
```
{% endcode %}

{% code title="File Upload to FTP server" %}
```bash
curl -T example.txt ftp://ftp.example.com/upload/
```
{% endcode %}

{% code title="File Upload + Custom HTTP Method" %}
```bash
curl -X PATCH -T example.txt https://example.com/upload
```
{% endcode %}
{% endhint %}

