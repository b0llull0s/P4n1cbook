---
icon: eye
description: Network Mapper
---

# Nmap

{% hint style="info" %}
## <mark style="color:purple;">Port Status</mark>

* <mark style="color:purple;">**`open`**</mark> -> _The connection through the NMAP scan has been successful._
* <mark style="color:purple;">**`closed`**</mark> -> _The port is closed._
* <mark style="color:purple;">**`filtered`**</mark> -> _Nmap does not know if the port is open or closed._
* <mark style="color:purple;">**`unfiltered`**</mark> _-> Port is accessible, but we don't know if it's open or closed._
* <mark style="color:purple;">**`open | filtered`**</mark> _-> This default state is assigned. It could be that a firewall is protecting the port._
* <mark style="color:purple;">**`closed | filtered`**</mark>** ->** _It's impossible to determine if the port is open or closed._
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">TCP Scans</mark>

{% code title="Connect Scan" %}
```bash
nmap -sT 192.168.1.1
```
{% endcode %}

{% code title="Specific Ports" %}
```bash
nmap -p 22,80,443 192.168.1.1
```
{% endcode %}

{% code title="All Ports" %}
```bash
nmap -p- 192.168.1.1
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

{% code title="Custom Source Port" %}
```bash
nmap --source-port 53 192.168.1.1
```
{% endcode %}

### <mark style="color:purple;">Timing and performance control</mark>

* <mark style="color:purple;">Timing templates go from</mark> <mark style="color:orange;">`0`</mark> <mark style="color:purple;">to</mark> <mark style="color:orange;">`5`</mark><mark style="color:purple;">, being</mark> <mark style="color:orange;">`3`</mark> <mark style="color:purple;">the default</mark>

{% code title="Set Timing Tables" %}
```bash
nmap -T4 192.168.1.1
```
{% endcode %}

{% code title="Very Fast Scan" %}
```bash
nmap -T5 192.168.1.1
```
{% endcode %}

{% code title="Very Slow Scan" %}
```bash
nmap -T0 192.168.1.1
```
{% endcode %}

{% code title="Control Parallelism" %}
```bash
nmap --min-parallelism 10 192.168.1.1
```
{% endcode %}

### <mark style="color:purple;">Host Discovery</mark>

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

{% code title="Random Host Scan with traceroute" %}
```bash
nmap -iR 10 -sn -traceroute
```
{% endcode %}

{% code title="Script for Discovery" %}
```bash
nmap --script discovery 192.168.1.1
```
{% endcode %}

### <mark style="color:purple;">DNS</mark>

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

### <mark style="color:purple;">Service and OS Detection</mark>

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

### <mark style="color:purple;">Examples</mark>

{% code title="Service and Version + Specific Port" %}
```bash
sudo nmap -sCV -oA nmap -p 'PORTS' [IP]
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">UDP Scans</mark>

{% code title="Basic Scan" %}
```bash
nmap -sU 192.168.1.1
```
{% endcode %}

{% code title="Specific Ports" %}
```bash
nmap -p 53,123,161 -sU 192.168.1.1
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

### <mark style="color:purple;">Host Discovery</mark>

{% code title="UDP Ping" %}
```bash
nmap 192.168.1.1-5 -PU53
```
{% endcode %}

### <mark style="color:purple;">Examples</mark>

{% code title="Specific Port + Scripts" %}
```bash
sudo nmap -sU -p 161 -sC 10.10.10.92
```
{% endcode %}
{% endhint %}

***

{% hint style="danger" %}
## <mark style="color:purple;">Stealth Scans</mark>

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

### <mark style="color:purple;">Examples</mark>

```bash
nmap -f -t 0 -n -Pn --data-length 200 -D 192.168.1.101,192.168.1.102,192.168.1.103,192.168.1.23 192.168.1.1
```
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">Scripting Engine (NSE)</mark>

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

{% code title="Category Of Scripts (Wildcard)" %}
```bash
nmap --script ssl* 192.168.1.1
```
{% endcode %}

{% code title="Script From File" %}
```bash
nmap --script /path/to/script.nse 192.168.1.1
```
{% endcode %}

### <mark style="color:purple;">Examples</mark>

{% code title="Safe SMB" %}
```bash
nmap -n -Pn -vv -O -sV -script smb-enum*,smb-ls,smb-mbenum,smb-os-discovery,smb-s*,smb-vuln*,smbv2* -vv 192.168.1.1
```
{% endcode %}

{% code title="HTTP Map Generator" %}
```bash
nmap -Pn -script=http-sitemap-generator scanme.nmap.org
```
{% endcode %}

{% code title="Fast Search For Random Web-Servers" %}
```bash
nmap -n -Pn -p 80 -open -sV -vvv -script banner,http-title -iR 1000
```
{% endcode %}

{% code title="Bruteforce DNS Hostname" %}
```bash
nmap -Pn -script=dns-brute domain.com
```
{% endcode %}

{% code title="Whois Query" %}
```bash
nmap -script whois* domain.com
```
{% endcode %}

{% code title="Cross Site Scripting" %}
```bash
nmap -p80 -script http-unsafe-output-escaping scanme.nmap.org
```
{% endcode %}

{% code title="SQLi" %}
```bash
nmap -p80 -script http-sql-injection scanme.nmap.org
```
{% endcode %}

{% code title="SNMP System Description" %}
```bash
nmap -script snmp-sysdescr -script-args snmpcommunity=admin 192.168.1.1
```
{% endcode %}

{% code title="SSH Brute Force" %}
```bash
nmap -n -p22 --script ssh-brute --script-args userdb=usernames.txt,passdb=passwords.txt <IP>
```
{% endcode %}

{% code title="CMS Configuration Backups" %}
```bash
nmap -n -p<PORT> --script http-config-backup <IP>
```
{% endcode %}

{% code title="Service Version and Vulnerabilities" %}
```bash
nmap -sV -p<PORT> --script vuln <IP>
```
{% endcode %}

{% code title="Wordpress Enumeration" %}
```bash
nmap -n -p<PORT> --script http-wordpress-enum <DNS>bash
```
{% endcode %}

{% code title="HeartBleed Vulnerability Check" %}
```bash
nmap -sV -p443 --script=ssl-heartbleed <DNS>
```
{% endcode %}

{% code title="Banner Grab" %}
```bash
nmap -n -p<PORT> --script dns-nsid <IP>
```
{% endcode %}

{% code title="Shellshock Vulnerability Check" %}
```bash
sudo nmap --script http-shellshock --script-args uri=<URL_ARCHIVO_SH> -p80 <IP>
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">Scan Output and Logging</mark>

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

### <mark style="color:purple;">Filtering Outputs</mark>

{% code title="Regex, Parse, Direct" %}
```bash
cat nmap.txt | grep -oP '([\d]+)/open' | awk -F/ '{print $1}' | tr '\n' ','       
```
{% endcode %}

{% code title="Removes Duplicates" %}
```bash
cat nmap.txt | grep open | grep -v '#' | cut -d"/" -f1 | sort | uniq | sed -z 's/\n/,/g;s/,$/\n/'
```
{% endcode %}

{% code title="Filtering Function" %}
```bash
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

### <mark style="color:purple;">Examples</mark>

{% code title="Web Server + Open Ports" %}
```bash
nmap -p80 -sV -oG - -open 192.168.1.1/24 | grep open
```
{% endcode %}

{% code title="Generate a list of the IPs live hosts" %}
```bash
nmap -iR 10 -n -oX out.xml | grep "Nmap" | cut -d " " -f5 > live-hosts.txt
```
{% endcode %}

{% code title="Append IP to the list of live hosts" %}
```bash
nmap -iR 10 -n -oX out2.xml | grep "Nmap" | cut -d " " -f5 >> live-hosts.txt
```
{% endcode %}

{% code title="Compare Output from Nmap" %}
```bash
ndiff scanl.xml scan2.xml
```
{% endcode %}

{% code title="Convert Nmap XML files to HTML files" %}
```bash
xsltproc nmap.xml -o nmap.html
```
{% endcode %}

{% code title="Reverse sorted list" %}
```bash
grep " open " results.nmap | sed -r ‘s/ +/ /g’ | sort | uniq -c | sort -rn | less
```
{% endcode %}
{% endhint %}

***

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







