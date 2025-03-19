---
description: Regular Expressions
---

# 💾 Regex

{% hint style="info" %}
## <mark style="color:red;">`Basic Tricks`</mark>

* <mark style="color:purple;">Look at uncommented lines from a file:</mark>

```sh
cat example | grep -Ev "^#" | grep .
```

* <mark style="color:purple;">Extracts only the text inside the quotes from a file:</mark>

```sh
sed 's/"\([^"]*\)"/\1/g' filename
```

* <mark style="color:purple;">Converting</mark> <mark style="color:orange;">**`Windows-style`**</mark> <mark style="color:purple;">line endings to</mark> <mark style="color:orange;">**`Unix-style`**</mark> <mark style="color:purple;">line endings:</mark>

```sh
sed -i 's/\r$//' file.sh
```

* <mark style="color:purple;">Execute a script on a loop until a condition is meet:</mark>

{% code overflow="wrap" %}
```sh
until ! ./poc.sh | grep -q "[x] ERROR"; do :; done; echo "No ERROR found, script finished successfully."
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:red;">`Making Wordlists`</mark>

* <mark style="color:purple;">Create wordlists for users and passwords from a dump file. The following code extracts the</mark> <mark style="color:orange;">**`first`**</mark> <mark style="color:purple;">(usernames) and</mark> <mark style="color:orange;">**`fourth`**</mark> <mark style="color:purple;">(password hashes) fields, which are separated by colons (</mark><mark style="color:orange;">**`:`**</mark><mark style="color:purple;">), and saves them into separate files:</mark>

```sh
awk '{print $1}' FS=':' dump.txt > users.txt
awk '{print $4}' FS=':' dump.txt > hashes.txt
```
{% endhint %}
