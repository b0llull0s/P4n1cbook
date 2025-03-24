---
description: Regular Expressions
---

# 💾 Regex

<details>

<summary><mark style="color:purple;"><strong><code>Basic Tricks</code></strong></mark></summary>

{% code title="Print uncommented lines" overflow="wrap" %}
```sh
cat example | grep -Ev "^#" | grep .
```
{% endcode %}

{% code title="Extracts text within quotes" %}
```sh
sed 's/"\([^"]*\)"/\1/g' filename
```
{% endcode %}

{% code title="Swap  to Unix-style" %}
```bash
sed -i 's/\r$//' file.sh
```
{% endcode %}

{% code title="Set a loop" overflow="wrap" %}
```sh
until ! ./poc.sh | grep -q "[x] ERROR"; do :; done; echo "No ERROR found, script finished successfully."
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Making Wordlists</code></strong></mark></summary>

<mark style="color:purple;">For example the following commands extracts the</mark> <mark style="color:purple;"></mark><mark style="color:purple;">**first**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">(</mark><mark style="color:orange;">**`usernames`**</mark><mark style="color:purple;">) and</mark> <mark style="color:purple;"></mark><mark style="color:purple;">**fourth**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">(</mark><mark style="color:red;">**`password hashes`**</mark><mark style="color:purple;">) fields, which are separated by colons (</mark><mark style="color:orange;">**`:`**</mark><mark style="color:purple;">):</mark>

```sh
awk '{print $1}' FS=':' dump.txt > users.txt
awk '{print $4}' FS=':' dump.txt > hashes.txt
```

</details>
