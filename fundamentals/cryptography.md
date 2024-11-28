---
icon: binary-lock
---

# Cryptography

{% hint style="info" %}
## <mark style="color:purple;">Checksum Validation</mark>

{% code title="Generate MD5 checksum" %}
```bash
md5sum file
```
{% endcode %}

{% code title="Generate SHA256 checksum" %}
```bash
sha256sum file
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">Certificates</mark>

### <mark style="color:purple;">Generate a Client Certificate</mark>

* <mark style="color:purple;">With the private key already, download the certificate from the page.</mark>
* <mark style="color:purple;">You can also look at the</mark> <mark style="color:orange;">**`client certificate requirements`**</mark><mark style="color:purple;">:</mark>

```bash
openssl s_client -connect 10.10.10.131:443
```

1. <mark style="color:purple;">Once you have all the pieces needed, Generate a 4096-bit RSA</mark> <mark style="color:orange;">**`private key`**</mark> <mark style="color:purple;">for the client:</mark>

```bash
openssl genrsa -out client.key 4096
```

2. <mark style="color:purple;">Create a</mark> <mark style="color:orange;">**`certificate signing request (CSR)`**</mark> <mark style="color:purple;">using the private key.</mark>

```bash
openssl req -new -key client.key -out client.req
```

3. <mark style="color:purple;">Sign the</mark> <mark style="color:orange;">**`CSR`**</mark> <mark style="color:purple;">with the</mark> <mark style="color:orange;">**`CA’s private key`**</mark> <mark style="color:purple;">to issue a</mark> <mark style="color:orange;">**`client certificate`**</mark> <mark style="color:purple;">valid for the desired time:</mark>

{% code overflow="wrap" %}
```bash
openssl x509 -req -in client.req -CA lacasadepapel-htb.pem -CAkey ca.key -set_serial 101 -extensions client -days 365 -outform PEM -out client.cer

```
{% endcode %}

4. <mark style="color:purple;">Convert the private key and certificate into a</mark> <mark style="color:orange;">**`PKCS#12 (.p12)`**</mark> <mark style="color:purple;">format file for easy import:</mark>

```bash
openssl pkcs12 -export -inkey client.key -in client.cer -out client.p12
```
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">File Signatures</mark>

* <mark style="color:purple;">Reads the first 16 bytes of a file and displays them in a hexadecimal format with</mark> <mark style="color:orange;">**`ASCII`**</mark> <mark style="color:purple;">representation:</mark>

```bash
file myfile && head -c 16 myfile | xxd
```

* <mark style="color:purple;">Converts the entire file into plain hex and extracts the first line:</mark>

```bash
xxd -p filename | head -n 1 
```
{% endhint %}



* **`ZIP`** --> `50 4B 03 04`

{% embed url="https://en.wikipedia.org/wiki/List_of_file_signatures" %}
