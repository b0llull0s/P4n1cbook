# 🦈 Wireshark

{% hint style="info" %}
## <mark style="color:purple;">Filters</mark>

### <mark style="color:purple;">Capture Filters</mark>

{% code title="Capture traffic from host" %}
```
host x.x.x.x
```
{% endcode %}

{% code title="Capture traffic from either directions" %}
```
net x.x.x.x/24
```
{% endcode %}

{% code title="Capture traffic from " %}
```
src net x.x.x.x/24
```
{% endcode %}

{% code title="Capture traffic to" %}
```
dst net x.x.x.x
```
{% endcode %}

* <mark style="color:purple;">Filter out all traffic except the port you specify:</mark>

```
port #
```

* <mark style="color:purple;">Will capture everything except the variable</mark>

```
not <variable>
```

* <mark style="color:purple;">Concatenate variables:</mark>

```
and
```

* <mark style="color:purple;">Grab traffic only within the range:</mark>

```
portrange x-x
```

* <mark style="color:purple;">Specify protocol filters:</mark>

```
ip / ether / tcp
```

* <mark style="color:purple;">Grabs a specific type of traffic:</mark>

```
broadcast / multicast / unicast
```

### <mark style="color:purple;">Display Filters</mark>

* <mark style="color:purple;">Capture only traffic pertaining to a certain host (</mark><mark style="color:orange;">**`OR`**</mark> <mark style="color:purple;">statement)</mark>

```
ip.addr == x.x.x.x
```

* <mark style="color:purple;">Capture traffic pertaining to a specific network(</mark><mark style="color:orange;">**`OR`**</mark> <mark style="color:purple;">statement)</mark>

```
ip.addr == x.x.x.x/24
```

* <mark style="color:purple;">Capture traffic to or from a specific host:</mark>

```
ip.src/dst == x.x.x.x
```

* <mark style="color:purple;">Filter traffic by protocol:</mark>

```
dns / tcp / ftp / arp / ip
```

* <mark style="color:purple;">Filter by a specific</mark> <mark style="color:orange;">**`TCP`**</mark> <mark style="color:purple;">port:</mark>

```
tcp.port == x
```

* <mark style="color:purple;">Will capture everything except the port specified:</mark>

```
src.port / dst.port ==x
```

* <mark style="color:orange;">**`AND`**</mark> <mark style="color:purple;">will concatenate,</mark> <mark style="color:orange;">**`OR`**</mark> <mark style="color:purple;">will find either of two options,</mark> <mark style="color:orange;">**`NOT`**</mark> <mark style="color:purple;">will exclude your input option:</mark>

```
and / or / not
```

* <mark style="color:purple;">Follow a</mark> <mark style="color:orange;">**`TCP`**</mark> <mark style="color:purple;">session stream:</mark>

```
tcp.stream eq #
```

* <mark style="color:purple;">Will filter for any traffic matching the</mark> <mark style="color:orange;">**`HTTP`**</mark><mark style="color:purple;">:</mark>

```
http
```

* <mark style="color:purple;">This filter will display any packet with a</mark> <mark style="color:orange;">**`JPEG`**</mark><mark style="color:purple;">:</mark>

```
http && image-jfif
```

* <mark style="color:purple;">Filters for the</mark> <mark style="color:orange;">**`FTP`**</mark> <mark style="color:purple;">protocol:</mark>

```
ftp
```

* <mark style="color:purple;">Will filter for any control commands sent over</mark> <mark style="color:orange;">**`FTP`**</mark> <mark style="color:purple;">control channel:</mark>

```
ftp.request.command
```

* <mark style="color:purple;">Will show any objects transferred over</mark> <mark style="color:orange;">**`FTP`**</mark>:

```
ftp-data
```
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:orange;">`tshark`</mark>

* <mark style="color:purple;">List available interfaces to capture from:</mark>

```sh
tshark -D
```

* <mark style="color:purple;">Capture on a selected interface:</mark>

```shell
tshark -i (int)
```

* <mark style="color:purple;">Apply a filter looking for a specific host:</mark>

```sh
tshark -i eth0 -f "host (ip)"
```

* <mark style="color:purple;">Will display any interfaces available to capture from and then exit out:</mark>

```
D
```

* <mark style="color:purple;">Will list the Link-layer mediums you can capture from and then exit out:</mark>

```
L
```

* <mark style="color:purple;">Defines a stop condition; Grab a specific number of packets, then quit the program :</mark>

```sh
c
```

* <mark style="color:purple;">Defines an auto-stop condition. It can be after a duration, specific file size, or after a certain number of packets:</mark>

```
a
```

* <mark style="color:purple;">Read from a file:</mark>

```sh
r (pcap-file)
```

* <mark style="color:purple;">Write into a file using the</mark> <mark style="color:orange;">**`pcapng`**</mark> <mark style="color:purple;">format:</mark>

```sh
W (pcap-file)
```

* <mark style="color:purple;">Will print the packet summary while writing into a file (</mark><mark style="color:orange;">**`-W`**</mark><mark style="color:purple;">):</mark>

```sh
P
```

* <mark style="color:purple;">Will add</mark> <mark style="color:orange;">**`Hex`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`ASCII`**</mark> <mark style="color:purple;">output into the capture:</mark>

```sh
x
```
{% endhint %}

***

## <mark style="color:purple;">Identifiers</mark>

{% hint style="info" %}
### <mark style="color:orange;">`FTP`</mark> <mark style="color:purple;">I</mark><mark style="color:purple;">**dentifiers**</mark>


{% endhint %}

