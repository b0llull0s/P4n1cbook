---
icon: eyes
---

# GoWitness

{% hint style="info" %}
### <mark style="color:red;">`Commands`</mark>

{% code title="Scan from file + Write to DB" overflow="wrap" %}
```sh
gowitness scan file -f urls.txt --write-db
```
{% endcode %}

{% code title="Scan a single site" overflow="wrap" %}
```shell
gowitness scan single --url "https://sensepost.com"
```
{% endcode %}

{% code title="Open Db File" overflow="wrap" %}
```sh
gowitness report list --db-uri sqlite://gowitness.sqlite3
```
{% endcode %}

{% code title="Start the report server" %}
```sh
gowitness report server
```
{% endcode %}
{% endhint %}

