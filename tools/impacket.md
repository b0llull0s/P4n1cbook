---
icon: bomb
---

# impacket

```
#Dumping Security
impacket-secretsdump LOCAL -system registry/SYSTEM -security registry/SECURITY

#Dumping ntds.dit
impacket-secretsdump LOCAL -ntds 'Active Directory/ntds.dit' -system 'registry/SYSTEM'

#Dumping and filtering
impacket-secretsdump LOCAL -ntds 'Active Directory/ntds.dit' -system 'registry/SYSTEM' | grep ::: > dump.txt
```
