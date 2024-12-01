---
icon: server
---

# MySQL

{% hint style="info" %}
## <mark style="color:purple;">Default Ports:</mark> <mark style="color:orange;">`3306`</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">`33060`</mark>

* <mark style="color:purple;">Use</mark> <mark style="color:orange;">**`ss -tlpn`**</mark> <mark style="color:purple;">**to check if is being run locally.**</mark>
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">Basic commands:</mark>

{% code title="Connect to the database" %}
```sh
mysql -u user -p
```
{% endcode %}

{% code title="Print available databases " %}
```sql
show databases;
```
{% endcode %}

{% code title="Connect to the database" %}
```sql
use databasename;
```
{% endcode %}

{% code title="Print tables from the database" %}
```sql
show tables;
```
{% endcode %}

{% code title="Print info about the table" %}
```sql
describe table_name;
```
{% endcode %}

{% code title="Print the selected parameters from table" %}
```sql
select name,username,password from sd4fg_users;
```
{% endcode %}

{% code title="Print all from table" %}
```sql
select * from table_name
```
{% endcode %}
{% endhint %}

