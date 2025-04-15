---
description: Network Mapper
icon: eye
---

# Nmap

<details>

<summary><mark style="color:purple;"><strong><code>Performance Tuning</code></strong></mark></summary>

{% hint style="info" %}
* <mark style="color:red;">**`Timing tables`**</mark> <mark style="color:purple;">go from</mark> <mark style="color:orange;">`0`</mark> <mark style="color:purple;">to</mark> <mark style="color:orange;">`5`</mark><mark style="color:purple;">, being</mark> <mark style="color:orange;">`3`</mark> <mark style="color:purple;">the default.</mark>

```bash
nmap -T4 192.168.1.1
```

* <mark style="color:orange;">**`--min-parallelism`**</mark> <mark style="color:purple;">allows to manually control the concurrency of the scan:</mark>

{% code overflow="wrap" %}
```bash
nmap -sS -T4 --min-parallelism 20 --max-retries 1 -p 80,443,22,3389 192.168.1.1
```
{% endcode %}

* <mark style="color:red;">**`Rate Limiting`**</mark>**&#x20;**<mark style="color:purple;">**(**</mark><mark style="color:orange;">**`--min-rate`**</mark><mark style="color:purple;">**/**</mark><mark style="color:orange;">**`--max-rate`**</mark><mark style="color:purple;">**)**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">gives you a better control over packets/second:</mark>

{% code overflow="wrap" %}
```bash
nmap -sS --min-rate 500 192.168.1.1
```
{% endcode %}

* <mark style="color:orange;">**`--max-rtt-timeout`**</mark>**&#x20;**<mark style="color:purple;">**a**</mark><mark style="color:purple;">djusts how long Nmap waits for responses before retrying:</mark>

{% code title="Optimized for LANs" %}
```sh
nmap -sS --max-rtt-timeout 200ms 192.168.1.1
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>TCP</code></strong></mark> <mark style="color:purple;"><strong>Scans</strong></mark></summary>

{% code title="Connect Scan" %}
```bash
nmap -sT -sV -p- 192.168.1.1
```
{% endcode %}

{% code title="ACK Scan" %}
```bash
nmap -sA 192.168.1.1
```
{% endcode %}

{% code title="Window Scan" %}
```bash
nmap -sW 192.168.1.1
```
{% endcode %}

{% code title="Maimon Scan" %}
```bash
nmap -sM 192.168.1.1
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Host Discovery</code></strong></mark></summary>

{% code title="Ping Sweep" %}
```bash
nmap -sn 192.168.1.0/24
```
{% endcode %}

{% code title="Disable Host Discovery" %}
```bash
nmap -Pn 192.168.1.0/24
```
{% endcode %}

{% code title="List targets Only" %}
```bash
nmap 192.168.1.1-3 -sL
```
{% endcode %}

{% code title="From Target File" %}
```bash
nmap -iL targets.txt
```
{% endcode %}

{% code title="Range Scan" %}
```bash
nmap 192.168.1.1-254
```
{% endcode %}

{% code title="TCP SYN Ping" %}
```bash
nmap 192.168.1.1-5 -PS22-25,80
```
{% endcode %}

{% code title="TCP ACK Ping" %}
```bash
nmap 192.168.1.1-5 -PA22-25,80
```
{% endcode %}

{% code title="ARP Ping" %}
```bash
nmap 192.168.1.1-1/24 -PR
```
{% endcode %}

{% code title="Ping Host (ICMP, ACK, ARP)" %}
```bash
nmap -PE -PA80 -PR 192.168.1.0/24
```
{% endcode %}

{% code title="Host Scan with traceroute" %}
```bash
nmap -iR 10 -sn -traceroute
```
{% endcode %}

{% code title="Script for Discovery" %}
```bash
nmap --script discovery 192.168.1.1
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>DNS</code></strong></mark> <mark style="color:purple;"><strong>Scans</strong></mark></summary>

{% code title="Standard Scan" %}
```bash
nmap --dns-servers 8.8.8.8 192.168.1.1
```
{% endcode %}

{% code title="Disable DNS Resolution" %}
```bash
nmap 192.168.1.1 -n
```
{% endcode %}

{% code title="Resolve Hostnames in a Range" %}
```bash
nmap 192.168.1.1-50 -sL -dns-server 192.168.1.1
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Service and OS Detection</code></strong></mark></summary>

{% code title="Service Version Detection" %}
```bash
nmap -sV 192.168.1.1
```
{% endcode %}

{% code title="OS Detection" %}
```bash
nmap -O 192.168.1.1
```
{% endcode %}

{% code title="Limits OS Detection" %}
```bash
nmap 192.168.1.1 -O -osscan-limit
```
{% endcode %}

{% code title="Aggressive Scan" %}
```bash
nmap -A 192.168.1.1
```
{% endcode %}

{% code title="Target Specific Ports" %}
```bash
sudo nmap -sCV -oA nmap -p 'PORTS' [IP]
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>UDP</code></strong></mark> <mark style="color:purple;"><strong>Scans</strong></mark></summary>

{% code title="Basic Scan" %}
```bash
nmap -sU 192.168.1.1
```
{% endcode %}

{% code title="Specific Ports" %}
```bash
nmap -p 53,123,161 -sU -sC 192.168.1.1
```
{% endcode %}

{% code title="All Ports" %}
```bash
nmap -p- -sU 192.168.1.1
```
{% endcode %}

{% code title="Service Detection" %}
```bash
nmap -sU -sV 192.168.1.1
```
{% endcode %}

{% code title="Script Scanning" %}
```bash
nmap -sU --script=udp* 192.168.1.1
```
{% endcode %}

{% hint style="info" %}
<mark style="color:red;">**`Host discovery for UDP`**</mark>

{% code title="UDP Ping first" overflow="wrap" %}
```sh
nmap -PU53,161,123 192.168.1.1-254 -oN udp_live_hosts.txt  
```
{% endcode %}

{% code title="Then scan live hosts" overflow="wrap" %}
```sh
nmap -sS -sV -p- -iL udp_live_hosts.txt -oA full_scan --max-retries 1  
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Stealthy Scans</code></strong></mark></summary>

{% hint style="info" %}
{% code title="Example" overflow="wrap" %}
```sh
nmap -f -t 0 -n -Pn --data-length 200 -D 192.168.1.101,192.168.1.102,192.168.1.103,192.168.1.23 192.168.1.1
```
{% endcode %}
{% endhint %}

{% code title="SYN Scan" %}
```bash
nmap -sS 192.168.1.1
```
{% endcode %}

{% code title="FIN Scan" %}
```bash
nmap -sF 192.168.1.1
```
{% endcode %}

{% code title="Xmas" %}
```bash
nmap -sX 192.168.1.1
```
{% endcode %}

{% code title="Scan with Decoys" %}
```bash
nmap -D RND:10 192.168.1.1
```
{% endcode %}

{% code title="Fragments Packets" %}
```bash
nmap -f 192.168.1.1
```
{% endcode %}

{% code title="Zombie Scan" %}
```bash
nmap -sI <zombie_host> 192.168.1.1
```
{% endcode %}

{% code title="Spoofed Source Address" %}
```bash
nmap -S 10.10.10.10 192.168.1.1
```
{% endcode %}

{% code title="Set Offset Size" %}
```bash
nmap 192.168.1.1 -mtu 32
```
{% endcode %}

{% code title="Specific Source Port" %}
```bash
nmap -g 53 192.168.1.1
```
{% endcode %}

{% code title="Use proxies" %}
```bash
nmap -proxies http://192.168.1.1:8080, http://192.168.1.2:8080 192.168.1.1
```
{% endcode %}

{% code title="Append Random Data" %}
```bash
nmap -data-length 200 192.168.1.1
```
{% endcode %}

{% code title="Non-intrusive Scripts" %}
```bash
nmap 192.168.1.1 -script "not intrusive"
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong>Scripting Engine -</strong></mark> <mark style="color:orange;"><strong><code>NSE</code></strong></mark></summary>

{% code title="List Scripts" %}
```bash
locate scripts/citrix
```
{% endcode %}

{% code title="Look At The Categories" %}
```bash
locate .nse | xargs grep "categories" | grep -oP '".*?"' | sort -u
```
{% endcode %}

{% code title="Look at any Specific category" %}
```bash
locate .nse | xargs grep -l 'categories =.*"discovery"'
```
{% endcode %}

{% code title="Default Scripts" %}
```bash
nmap -sC 192.168.1.1
```
{% endcode %}

{% code title="Specific Script" %}
```bash
nmap --script smb-vuln* 192.168.1.1
```
{% endcode %}

{% code title="Version and Vulnerabilities" overflow="wrap" %}
```sh
nmap -sV -p<PORT> --script vuln <IP>
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Outputs</code></strong></mark></summary>

{% code title="Normal Output" %}
```bash
nmap -oN output.txt 192.168.1.1
```
{% endcode %}

{% code title="XML Output" %}
```bash
nmap -oX output.xml 192.168.1.1
```
{% endcode %}

{% code title="All formats" %}
```bash
nmap -oA output_prefix 192.168.1.1
```
{% endcode %}

{% code title="Grepable Output" %}
```bash
nmap -oG output.txt 192.168.1.1
```
{% endcode %}

{% hint style="info" %}
<mark style="color:red;">**`Filtering`**</mark>

{% code title="Regex, Parse, Direct" overflow="wrap" %}
```sh
cat nmap.txt | grep -oP '([\d]+)/open' | awk -F/ '{print $1}' | tr '\n' ','
```
{% endcode %}

{% code title="Removes Duplicates" overflow="wrap" %}
```sh
cat nmap.txt | grep open | grep -v '#' | cut -d"/" -f1 | sort | uniq | sed -z 's/\n/,/g;s/,$/\n/'
```
{% endcode %}

{% code title="Filtering Function" overflow="wrap" %}
```sh
function extractPorts(){
	ports="$(cat $1 | grep -oP '\d{1,5}/open' | awk '{print $1}' FS='/' | xargs | tr ' ' ',')"
	ip_address="$(cat $1 | grep -oP '\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}' | sort -u | head -n 1)"
	echo -e "\n[*] Extracting information...\n" > extractPorts.tmp
	echo -e "\t[*] IP Address: $ip_address"  >> extractPorts.tmp
	echo -e "\t[*] Open ports: $ports\n"  >> extractPorts.tmp
	echo $ports | tr -d '\n' | xclip -sel clip
	echo -e "[*] Ports copied to clipboard\n"  >> extractPorts.tmp
	cat extractPorts.tmp; rm extractPorts.tmp
}
```
{% endcode %}

{% code title="Reverse sorted list" overflow="wrap" %}
```sh
grep " open " results.nmap | sed -r ‘s/ +/ /g’ | sort | uniq -c | sort -rn | less
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
<mark style="color:red;">**`Generate a IPs live hosts list`**</mark>

{% code overflow="wrap" %}
```sh
nmap -iR 10 -n -oX out.xml | grep "Nmap" | cut -d " " -f5 > live-hosts.txt
```
{% endcode %}

{% code title="Append IPs" overflow="wrap" %}
```sh
nmap -iR 10 -n -oX out2.xml | grep "Nmap" | cut -d " " -f5 >> live-hosts.txt
```
{% endcode %}
{% endhint %}

</details>

{% hint style="info" %}
## <mark style="color:purple;">Other Techniques</mark>

{% code title="TCP and UDP" %}
```bash
nmap 192.168.1.1 -p U:53,T:21-25,80
```
{% endcode %}

{% code title="IPv6" %}
```bash
nmap -6 2607:f0d0:1002:51::4
```
{% endcode %}
{% endhint %}







