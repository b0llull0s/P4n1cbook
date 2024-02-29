# 🔑 Brute-Forcing

### <mark style="color:purple;">Libraries</mark>



### JohnTheRipper

**John**

```bash
#From list
john -w=/usr/share/wordlists/seclists/Passwords/Leaked-Databases/rockyou.txt hash

#From zip hash
john <file>.john --wordlist=/usr/share/wordlists/rockyou.txt
```

**ZIP to John**

```bash
zip2john <file> > <newfile>.john
```
