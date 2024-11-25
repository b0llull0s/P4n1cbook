---
icon: binary-lock
---

# Cryptography

{% hint style="info" %}
## <mark style="color:purple;">`base64`</mark>

{% code title="Encode + Append to a file" %}
```basic
base64 file.txt > hash.txt
```
{% endcode %}

{% code title="Encode + Create file" %}
```bash
echo "your_string_here" | base64 > encoded_file.txt
```
{% endcode %}

{% code title="Encode file" %}
```bash
cat <file> | base64 -w 0; echo
```
{% endcode %}

{% code title="Prevent line wrapping" %}
```bash
base64 -w 0 <file>
```
{% endcode %}

{% code title="Decode String" %}
```bash
echo <string> | base64 -d > <file>
```
{% endcode %}
{% endhint %}

<mark style="color:red;">`md5sum`</mark> <mark style="color:purple;">--></mark> <mark style="color:purple;"></mark><mark style="color:purple;">**SHA256 CheckSum**</mark>

{% hint style="info" %}
## File Signatures

{% code title="view the first few bites from a file" %}
```bash
xxd -p filename | head -n 1 
```
{% endcode %}
{% endhint %}



### File Signatures:

```
head -c 16 file | xxd
```

* **`ZIP`** --> `50 4B 03 04`

{% embed url="https://en.wikipedia.org/wiki/List_of_file_signatures" %}
