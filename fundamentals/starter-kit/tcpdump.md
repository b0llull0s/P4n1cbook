---
icon: binary
---

# tcpdump

{% hint style="info" %}
### <mark style="color:purple;">`Commands`</mark>

* <mark style="color:purple;">Prints the</mark> <mark style="color:orange;">**`tcpdump`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`libpcap`**</mark> <mark style="color:purple;">version strings then exits:</mark>

```sh
tcpdump --version
```

* <mark style="color:purple;">Prints a list of usable network interfaces to capture from:</mark>

```sh
tcpdump -D
```

* <mark style="color:purple;">Utilizes the interface specified to capture on:</mark>

```sh
tcpdump -i InterfaceName
```

* <mark style="color:purple;">Combine Filters Using AND (</mark><mark style="color:orange;">**`&&`**</mark><mark style="color:purple;">)</mark>

```sh
tcpdump src host 192.168.1.1 && port 80
```

* <mark style="color:purple;">Combine Filters Using OR (</mark><mark style="color:orange;">**`or`**</mark><mark style="color:purple;">)</mark>

```shell
tcpdump src host 192.168.1.1 or dst host 192.168.1.2
```

* <mark style="color:purple;">Exclude Specific Traffic Using NOT (</mark><mark style="color:orange;">**`not`**</mark><mark style="color:purple;">)</mark>

```sh
tcpdump not udp
```

* <mark style="color:purple;">Do Not Resolve</mark> <mark style="color:orange;">**`Hostnames`**</mark>:

```sh
tcpdump -n
```

* <mark style="color:purple;">Do Not Resolve</mark> <mark style="color:orange;">**`Hostnames`**</mark> <mark style="color:purple;">or</mark> <mark style="color:orange;">**`Ports`**</mark><mark style="color:purple;">:</mark>

```sh
tcpdump -nn
```

* <mark style="color:purple;">Capture</mark> <mark style="color:orange;">**`Ethernet`**</mark> <mark style="color:purple;">Headers and Data:</mark>

```sh
tcpdump -e
```

* <mark style="color:purple;">Show Packet Contents in</mark> <mark style="color:orange;">**`Hex`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`ASCII`**</mark><mark style="color:purple;">:</mark>

```sh
tcpdump -X
```

* <mark style="color:purple;">Show</mark> <mark style="color:orange;">**`Ethernet`**</mark> <mark style="color:purple;">Header + Packet Contents in</mark> <mark style="color:orange;">**`Hex`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`ASCII`**</mark>

```sh
tcpdump -XX
```

* <mark style="color:purple;">Increase</mark> <mark style="color:orange;">**`Verbosity`**</mark><mark style="color:purple;">**:**</mark>

```sh
tcpdump -v
tcpdump -vv
tcpdump -vvv
```

* <mark style="color:purple;">Capture a Specific</mark> <mark style="color:orange;">**`Number of Packets`**</mark><mark style="color:purple;">:</mark>

```sh
tcpdump -c 10
```

* <mark style="color:purple;">Limit the Amount of Data to Capture from Each Packet:</mark>

```sh
tcpdump -s 64
```

* <mark style="color:purple;">Filter by</mark> <mark style="color:orange;">**`Packet Size`**</mark><mark style="color:purple;">:</mark>

```bash
tcpdump greater 1000
tcpdump less 500
```

* <mark style="color:purple;">Show Absolute Sequence Numbers in</mark> <mark style="color:orange;">**`TCP`**</mark><mark style="color:purple;">:</mark>

```sh
tcpdump -S
```

* <mark style="color:purple;">Reduce Protocol Information in the Output:</mark>

```sh
tcpdump -q
```

* <mark style="color:purple;">Filter by</mark> <mark style="color:orange;">**`Source`**</mark> <mark style="color:purple;">or</mark> <mark style="color:orange;">**`Destination`**</mark> <mark style="color:purple;">Host:</mark>

```sh
tcpdump src host 192.168.1.1
tcpdump dst host 192.168.1.1
```

* <mark style="color:purple;">Filter by</mark> <mark style="color:orange;">**`Network`**</mark>

```sh
tcpdump net 192.168.1.0/24
```

* <mark style="color:purple;">Runs a capture on the specified interface and writes the output to a file:</mark>

```sh
tcpdump -i InterfaceName -w file.pcap
```

* <mark style="color:purple;">Read the output from a specified file:</mark>

```sh
tcpdump -r file.pcap
```

* <mark style="color:purple;">Write Packets to a File</mark>

```sh
tcpdump -w capture_file.pcap
```

* <mark style="color:purple;">Only capture traffic originating</mark> <mark style="color:orange;">**`from`**</mark> <mark style="color:purple;">or destined</mark> <mark style="color:orange;">**`to`**</mark> <mark style="color:purple;">the</mark> <mark style="color:orange;">**`IP`**</mark> <mark style="color:purple;">address or</mark> <mark style="color:orange;">**`hostname`**</mark> <mark style="color:purple;">specified:</mark>

```sh
tcpdump -i (int) host (ip)
```

* <mark style="color:purple;">Will filter the capture for anything sourcing</mark> <mark style="color:orange;">**`from`**</mark> <mark style="color:purple;">or destined</mark> <mark style="color:orange;">**`to`**</mark> <mark style="color:orange;">**`port`**</mark><mark style="color:purple;">:</mark>

```sh
tcpdump -i (int) port (#)
```

* <mark style="color:purple;">Filter by</mark> <mark style="color:orange;">**`Port Range`**</mark>

```sh
tcpdump portrange 1000-2000
```

* <mark style="color:purple;">Will utilize a protocols common name to filter the traffic captured:</mark>

```sh
tcpdump -i (int) proto ICMP
```

* <mark style="color:purple;">Will filter the capture for any protocol traffic matching their code:</mark>

```sh
tcpdump -i (int) proto 6
```

***

### <mark style="color:purple;">`Protocol Number List`</mark>

* <mark style="color:orange;">**`ICMP`**</mark>**&#x20;**<mark style="color:purple;">**(Internet Control Message Protocol) ->**</mark>**&#x20;**<mark style="color:orange;">**`1`**</mark>
* <mark style="color:orange;">**`IGMP`**</mark> <mark style="color:purple;">**(Internet Group Management Protocol) ->**</mark> <mark style="color:orange;">**`2`**</mark>
* <mark style="color:orange;">**`TCP`**</mark> <mark style="color:purple;">**(Transmission Control Protocol) ->**</mark> <mark style="color:orange;">**`6`**</mark>
* <mark style="color:orange;">**`UDP`**</mark>**&#x20;**<mark style="color:purple;">**(User Datagram Protocol) ->**</mark>**&#x20;**<mark style="color:orange;">**`17`**</mark>
* <mark style="color:orange;">**`OSPF`**</mark>**&#x20;**<mark style="color:purple;">**(Open Shortest Path First) ->**</mark>**&#x20;**<mark style="color:orange;">**`89`**</mark>
* <mark style="color:orange;">**`EIGRP`**</mark>**&#x20;**<mark style="color:purple;">**(Enhanced Interior Gateway Routing Protocol) ->**</mark>**&#x20;**<mark style="color:orange;">**`88`**</mark>
* <mark style="color:orange;">**`AH`**</mark>**&#x20;**<mark style="color:purple;">**(Authentication Header) ->**</mark>**&#x20;&#x20;**<mark style="color:orange;">**`51`**</mark>
* <mark style="color:orange;">**`ESP`**</mark>**&#x20;**<mark style="color:purple;">**(Encapsulating Security Payload) ->**</mark>**&#x20;**<mark style="color:orange;">**`50`**</mark>
* <mark style="color:orange;">**`GRE`**</mark>**&#x20;**<mark style="color:purple;">**(Generic Routing Encapsulation) ->**</mark>**&#x20;**<mark style="color:orange;">**`47`**</mark>
* <mark style="color:orange;">**`IPv6`**</mark>**&#x20;**<mark style="color:purple;">**(Internet Protocol version 6) ->**</mark>**&#x20;**<mark style="color:orange;">**`41`**</mark>
* <mark style="color:orange;">**`IPv4`**</mark>**&#x20;**<mark style="color:purple;">**(Internet Protocol version 4) ->**</mark>**&#x20;**<mark style="color:orange;">**`4`**</mark>
* <mark style="color:orange;">**`DCCP`**</mark>**&#x20;**<mark style="color:purple;">**(Datagram Congestion Control Protocol) ->**</mark>**&#x20;**<mark style="color:orange;">**`33`**</mark>
* <mark style="color:orange;">**`SCTP`**</mark>**&#x20;**<mark style="color:purple;">**(Stream Control Transmission Protocol) ->**</mark>**&#x20;**<mark style="color:orange;">**`132`**</mark>
* <mark style="color:orange;">**`RARP`**</mark>**&#x20;**<mark style="color:purple;">**(Reverse Address Resolution Protocol) ->**</mark>**&#x20;**<mark style="color:orange;">**`3`**</mark>
* <mark style="color:orange;">**`PPTP`**</mark>**&#x20;**<mark style="color:purple;">**(Point-to-Point Tunneling Protocol) ->**</mark>**&#x20;**<mark style="color:orange;">**`115`**</mark>
* <mark style="color:orange;">**`MPLS`**</mark>**&#x20;**<mark style="color:purple;">**(Multiprotocol Label Switching) ->**</mark>**&#x20;**<mark style="color:orange;">**`89`**</mark>
* <mark style="color:orange;">**`X.25`**</mark>**&#x20;**<mark style="color:purple;">**->**</mark>**&#x20;**<mark style="color:orange;">**`93`**</mark>
* <mark style="color:orange;">**`FDDI`**</mark>**&#x20;**<mark style="color:purple;">**(Fiber Distributed Data Interface) ->**</mark>**&#x20;**<mark style="color:orange;">**`97`**</mark>
{% endhint %}

