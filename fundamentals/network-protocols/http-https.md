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

* <mark style="color:purple;">The config file normally lives in</mark> <mark style="color:orange;">**`/etc/squid/squid.conf`**</mark>&#x20;
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

