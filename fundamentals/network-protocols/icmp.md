---
icon: hand-point-right
description: Internet Control Message Protocol
---

# ICMP

<mark style="color:purple;">It is used by</mark> [<mark style="color:purple;">network devices</mark>](https://en.wikipedia.org/wiki/Network_device)<mark style="color:purple;">, including</mark> [<mark style="color:purple;">routers</mark>](https://en.wikipedia.org/wiki/Router_\(computing\))<mark style="color:purple;">, to send error messages and operational information indicating success or failure when communicating with another</mark> [<mark style="color:purple;">IP address</mark>](https://en.wikipedia.org/wiki/IP_address)<mark style="color:purple;">.</mark>

<mark style="color:orange;">**`ICMP`**</mark> <mark style="color:purple;">differs from</mark> [<mark style="color:purple;">transport protocols</mark>](https://en.wikipedia.org/wiki/Transport_protocol) <mark style="color:purple;">such as</mark> [<mark style="color:orange;">**`TCP`**</mark>](https://en.wikipedia.org/wiki/Transmission_Control_Protocol) <mark style="color:purple;">and</mark> [<mark style="color:orange;">**`UDP`**</mark>](https://en.wikipedia.org/wiki/User_Datagram_Protocol) <mark style="color:purple;">in that it is not typically used to exchange data between systems, nor is it regularly employed by end-user network applications (with the exception of some diagnostic tools like</mark> [<mark style="color:orange;">**`ping`**</mark>](https://en.wikipedia.org/wiki/Ping_\(networking_utility\)) <mark style="color:purple;">and</mark> [<mark style="color:orange;">**`traceroute`**</mark>](https://en.wikipedia.org/wiki/Traceroute)<mark style="color:purple;">).</mark>

<mark style="color:purple;">A separate Internet Control Message Protocol (called</mark> [<mark style="color:orange;">**`ICMPv6`**</mark>](https://en.wikipedia.org/wiki/ICMPv6)<mark style="color:purple;">) is used with</mark> [<mark style="color:orange;">**`IPv6`**</mark>](https://en.wikipedia.org/wiki/IPv6)<mark style="color:purple;">.</mark>

{% embed url="https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol" %}

***

{% hint style="info" %}
### <mark style="color:orange;">`ping`</mark>

* <mark style="color:purple;">Used to test connectivity between devices on a network.</mark>
* <mark style="color:purple;">It sends</mark> <mark style="color:orange;">**`ICMP Echo Request`**</mark> <mark style="color:purple;">packets to a target and waits for</mark> <mark style="color:orange;">**`ICMP Echo Reply`**</mark> <mark style="color:purple;">packets in return.</mark>
* <mark style="color:purple;">The command provides details like packet loss, round-trip time (</mark><mark style="color:orange;">**`RTT`**</mark><mark style="color:purple;">), and</mark> <mark style="color:orange;">**`TTL`**</mark> <mark style="color:purple;">(time-to-live).</mark>

***

{% code title="Output Example" overflow="wrap" %}
```sh
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.123 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.120 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=0.122 ms
```
{% endcode %}

* <mark style="color:orange;">**`Bytes`**</mark><mark style="color:purple;">: Size of the</mark> <mark style="color:orange;">**`ICMP`**</mark> <mark style="color:purple;">packet.</mark>
* <mark style="color:orange;">**`From`**</mark><mark style="color:purple;">: IP address of the responding device.</mark>
* <mark style="color:orange;">**`icmp_seq`**</mark><mark style="color:purple;">: Sequence number of the packet.</mark>
* <mark style="color:orange;">**`TTL`**</mark>**&#x20;**<mark style="color:purple;">**(Time to Live)**</mark><mark style="color:purple;">: The maximum number of hops a packet can traverse before being discarded.</mark>
* <mark style="color:orange;">**`Time`**</mark><mark style="color:purple;">: The round-trip time (</mark><mark style="color:orange;">**`RTT`**</mark><mark style="color:purple;">) for the packet to reach the destination and return.</mark>

***

### <mark style="color:orange;">`TTL`</mark> <mark style="color:purple;">Values and</mark> <mark style="color:orange;">`OS`</mark> <mark style="color:purple;">Fingerprinting</mark>

* <mark style="color:purple;">The</mark> <mark style="color:orange;">**`TTL`**</mark> <mark style="color:purple;">value in the ping response is a starting value decremented by one for each hop the packet takes.</mark>
* <mark style="color:purple;">The default starting</mark> <mark style="color:orange;">**`TTL`**</mark> <mark style="color:purple;">values differ between operating systems, making it possible to infer the</mark> <mark style="color:orange;">**`OS`**</mark> <mark style="color:purple;">of the target system.</mark>
  * <mark style="color:orange;">**`Linux/Unix`**</mark> <mark style="color:purple;">-></mark> <mark style="color:orange;">**`64`**</mark>
  * <mark style="color:orange;">**`Windows`**</mark> <mark style="color:purple;">-></mark> <mark style="color:orange;">**`128`**</mark>
  * <mark style="color:orange;">**`Cisco`**</mark> <mark style="color:purple;">-></mark> <mark style="color:orange;">**`255`**</mark>

***

### <mark style="color:purple;">Commands</mark>

{% code title="Send 4 packages" overflow="wrap" %}
```sh
ping -c 4 example.com
```
{% endcode %}

```
// Some c
```
{% endhint %}

