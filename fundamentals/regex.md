---
description: Regular Expressions
---

# 💾 Regex

{% hint style="info" %}
## Basic Tricks

{% code title="Match delimiters content "" %}
```regex
[^"]+
```
{% endcode %}

* <mark style="color:purple;">Removes all</mark> <mark style="color:orange;">**`/r`**</mark> <mark style="color:purple;">from the target file</mark>

```
sed -i 's/\r$//' file.sh
```
{% endhint %}



```

#Making a diccionary (arguments 1 and 4)
awk '{print $1}' FS=':' dump.txt > users.txt
awk '{print $4}' FS=':' dump.txt > hashes.txt
```

