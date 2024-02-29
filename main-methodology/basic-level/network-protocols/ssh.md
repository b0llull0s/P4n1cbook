# SSH

Nmap SSH vulnerability scansh:

```
nmap -sV -p22 -Pn --script vuln 10.10.11.233

```

Uses:

```
#Username
ssh -l {USERNAME} {IP}
#With key.file
ssh -i {filename} {user}@{IPADDRESS}
```

<mark style="color:purple;">**OpenSSH Vulnerabilities Repology**</mark>

{% embed url="https://repology.org/project/openssh/cves?version=8.9.p1" %}
