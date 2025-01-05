---
icon: knife-kitchen
hidden: true
---

# JohnTheRipper

Hash

```bash
#Generate a hash
md5sum

#Generate a hash from a zipfile
zip2john <file> > <newfile>.john
```

John

```bash
#From list
john -w=/usr/share/wordlists/seclists/Passwords/Leaked-Databases/rockyou.txt hash

#From zip hash
john <file>.john --wordlist=/usr/share/wordlists/rockyou.txt
```
