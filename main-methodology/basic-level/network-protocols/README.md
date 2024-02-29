---
description: Scrips and sheets
---

# 🌐 Network Protocols

### <mark style="color:purple;">**Nmap:**</mark>

<mark style="color:purple;">**TCP**</mark>

```python
#Port Scanner with scripts
sudo nmap -Pn -sCV -oN nmap.txt
# For every Port
sudo nmap -p- -Pn -sCV -oN nmap.txt
#Specific Ports
nmap <IP> -p <Ports> -sCV -T4 -oN vulns
```

<mark style="color:purple;">**CTF:**</mark>

```bash
#Very Noise Scanner
nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn <IP> -oG allPorts
#Even faster way
nmap -sT -p- --min-rate 10000 -vvv <ip> -oG nmap.txt
```

<mark style="color:purple;">**UDP**</mark>

```bash
#X 100/500
sudo nmap -sU --top-ports X --open -T5 -v -n <IP>
#100 top tipical ports
sudo nmap -sU -T5 -Pn -n -v --top-ports 100 <IP>

#Specific port with scripts
sudo nmap -sU -p 161 -sC 10.10.10.92
```

#### IPv6:

```
#Release current IPv6
sudo dhclient -6 -r 
#Renew IPv6
sudo dhclient -6 
```

DHCP:

```
#send a DHCP request (renew the lease)
sudo dhclient -v
```

