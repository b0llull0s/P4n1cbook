---
icon: diagram-project
---

# Network Analysis

{% hint style="info" %}
<mark style="color:purple;">**Use**</mark>**&#x20;**<mark style="color:orange;">**`lft`**</mark>**&#x20;**<mark style="color:purple;">**to trace hops in the network**</mark>

```sh
sudo lft <IP:PORT>
```

* <mark style="color:purple;">If you suspect that there is a</mark> <mark style="color:orange;">**`VM`**</mark> <mark style="color:purple;">or</mark> <mark style="color:orange;">**`docker`**</mark> <mark style="color:purple;">being hosted in a different port you can use</mark> <mark style="color:orange;">**`lft`**</mark> <mark style="color:purple;">and check if there are differences in  the results.</mark>
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">**Find the processes associated with a port**</mark>

```sh
lsof -i -n -P <port_number>
```

<mark style="color:purple;">**Shows**</mark>**&#x20;**<mark style="color:orange;">**`TCP`**</mark>**&#x20;**<mark style="color:purple;">**open connections in the Listen state**</mark>

```sh
lsof -wnP -iTCP -sTCP:LISTEN
```
{% endhint %}

<details>

<summary><mark style="color:orange;"><strong><code>ip</code></strong></mark></summary>

{% code title="Bring interface up" overflow="wrap" %}
```bash
sudo ip link set eth0 up
```
{% endcode %}

{% code title="Display the Routing Table" %}
```bash
ip route show
```
{% endcode %}

{% code title="Add a route" %}
```bash
sudo ip route add 192.168.2.0/24 via 192.168.1.254
```
{% endcode %}

{% code title="Delete a Route" %}
```bash
sudo ip route del 192.168.2.0/24
```
{% endcode %}

{% code title="Add a Default Gateway" %}
```bash
sudo ip route add default via 192.168.1.1
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>ping</code></strong></mark></summary>

{% hint style="info" %}
<mark style="color:red;">**`Ping and TCPdump Network Analysis for RCE Detection`**</mark>

* <mark style="color:purple;">Simply</mark> <mark style="color:orange;">**`ping`**</mark> <mark style="color:purple;">your own host, you can use the command directly or as a payload for a script:</mark>

```bash
ping -c 1 10.10.14.6
```

* <mark style="color:purple;">And catch it with</mark> <mark style="color:orange;">**`tcpdump`**</mark><mark style="color:purple;">**:**</mark>

```bash
sudo tcpdump -ni <interface> icmp
```
{% endhint %}

{% hint style="info" %}
<mark style="color:orange;">**`TTL`**</mark>**&#x20;**<mark style="color:purple;">**Values and**</mark>**&#x20;**<mark style="color:orange;">**`OS`**</mark>**&#x20;**<mark style="color:purple;">**Fingerprinting**</mark>

* <mark style="color:purple;">The</mark> <mark style="color:orange;">**`TTL`**</mark> <mark style="color:purple;">value in the ping response is a starting value decremented by one for each hop the packet takes; Values differ between operating systems:</mark>
* <mark style="color:orange;">**`Linux/Unix`**</mark> <mark style="color:purple;">-></mark> <mark style="color:orange;">**`64`**</mark>
* <mark style="color:orange;">**`Windows`**</mark> <mark style="color:purple;">-></mark> <mark style="color:orange;">**`128`**</mark>
* <mark style="color:orange;">**`Cisco`**</mark> <mark style="color:purple;">-></mark> <mark style="color:orange;">**`255`**</mark>
{% endhint %}

{% code title="Send 4 packages" overflow="wrap" %}
```bash
ping -c 4 example.com
```
{% endcode %}

{% hint style="info" %}
* <mark style="color:purple;">It sends</mark> <mark style="color:orange;">**`ICMP Echo Request`**</mark> <mark style="color:purple;">packets to a target and waits for</mark> <mark style="color:orange;">**`ICMP Echo Reply`**</mark> <mark style="color:purple;">packets in return.</mark>

{% code title="Output Example" overflow="wrap" %}
```bash
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.123 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.120 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=0.122 ms
```
{% endcode %}

* <mark style="color:orange;">**`TTL`**</mark>**&#x20;**<mark style="color:purple;">**(Time to Live)**</mark><mark style="color:purple;">: The maximum number of hops a packet can traverse before being discarded.</mark>
* <mark style="color:orange;">**`Time`**</mark><mark style="color:purple;">: The round-trip time (</mark><mark style="color:orange;">**`RTT`**</mark><mark style="color:purple;">) for the packet to reach the destination and return.</mark>
{% endhint %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>ss</code></strong></mark></summary>

{% code title="Listening ports & services" %}
```bash
ss -tuln
```
{% endcode %}

{% code title="Listening ports + PID" %}
```bash
ss -tulnp | grep PID
```
{% endcode %}

{% code title="Trace the network path" %}
```bash
traceroute example.com
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>tripwire</code></strong></mark></summary>

{% code title="Initialize the Tripwire database" %}
```bash
sudo tripwire --init
```
{% endcode %}

{% code title="Check the integrity of the system" %}
```bash
sudo tripwire --check
```
{% endcode %}

{% code title="Generate a report" %}
```bash
sudo tripwire --update
```
{% endcode %}

</details>
