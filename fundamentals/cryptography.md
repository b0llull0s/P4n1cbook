---
icon: binary-lock
---

# Cryptography

{% hint style="info" %}
## <mark style="color:purple;">File Signatures</mark>

* <mark style="color:purple;">Reads the first 16 bytes of a file and displays them in a hexadecimal format with</mark> <mark style="color:orange;">**`ASCII`**</mark> <mark style="color:purple;">representation:</mark>

```bash
file myfile && head -c 16 myfile | xxd
```

* <mark style="color:purple;">Converts the entire file into plain hex and extracts the first line:</mark>

```bash
xxd -p filename | head -n 1 
```
{% endhint %}

{% embed url="https://en.wikipedia.org/wiki/List_of_file_signatures" %}
