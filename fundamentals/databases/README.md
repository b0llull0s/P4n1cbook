---
icon: database
description: Structure Query Language
---

# Databases

{% hint style="warning" %}
* <mark style="color:purple;">SQL queries are sent over</mark> <mark style="color:orange;">**`TCP/IP`**</mark>
* <mark style="color:purple;">SQL can transported over</mark> <mark style="color:orange;">**`HTTP`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`HTTPS`**</mark><mark style="color:purple;">, or custom protocols designed for database communication.</mark>
* <mark style="color:purple;">SQL can be wrapped in other protocols (e.g.,</mark> <mark style="color:orange;">**`ODBC`**</mark>, <mark style="color:orange;">**`JDBC`**</mark><mark style="color:purple;">)</mark>
{% endhint %}

{% tabs %}
{% tab title="SQL Server" %}
{% code title="Port" %}
```
1433
```
{% endcode %}
{% endtab %}

{% tab title="MySQL" %}
{% code title="Port" %}
```
3306
```
{% endcode %}

{% hint style="warning" %}
<mark style="color:purple;">Same as</mark> <mark style="color:orange;">**`MariaDb`**</mark>
{% endhint %}
{% endtab %}

{% tab title="PostgreSQL" %}
{% code title="Port" %}
```
5432
```
{% endcode %}
{% endtab %}

{% tab title="MSSQL" %}
{% code title="TCP Port" %}
```
1433
```
{% endcode %}

{% code title="UDP Port" %}
```
1434
```
{% endcode %}
{% endtab %}

{% tab title="Oracle" %}
{% code title="Port" %}
```
1521
```
{% endcode %}
{% endtab %}

{% tab title="IBM DB2" %}
{% code title="TCP Port" %}
```
50000
```
{% endcode %}
{% endtab %}
{% endtabs %}
