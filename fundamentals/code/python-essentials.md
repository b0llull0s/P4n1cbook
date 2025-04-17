---
icon: snake
---

# Python Essentials

<details>

<summary><mark style="color:purple;"><strong><code>Virtual Environment</code></strong></mark></summary>

{% code title="Create the environment" overflow="wrap" %}
```sh
python -m venv env_name
```
{% endcode %}

{% code title="Activate it" overflow="wrap" %}
```sh
source env_name/bin/activate
```
{% endcode %}

{% code title="Install requirements" overflow="wrap" %}
```sh
pip install -r requirements.txt
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Libraries</code></strong></mark></summary>

{% code title="Check Library Version" overflow="wrap" %}
```bash
pip show <library_name>
```
{% endcode %}

{% hint style="info" %}
#### <mark style="color:red;">`urllib3`</mark>

<mark style="color:purple;">Disable</mark> <mark style="color:orange;">**`SSL`**</mark> <mark style="color:purple;">warnings for insecure connections:</mark>

{% code overflow="wrap" %}
```python
import urllib3
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
#### <mark style="color:red;">**`pymysql`**</mark>

<mark style="color:purple;">Python client for interacting with</mark> <mark style="color:orange;">**`MySQL`**</mark> <mark style="color:purple;">databases.</mark>

* <mark style="color:purple;">The following script dynamically executes</mark> <mark style="color:orange;">**`SQL`**</mark> <mark style="color:purple;">queries on a target database using credentials extracted from application settings.</mark>
* &#x20;<mark style="color:purple;">It need to be in a directory where the</mark> <mark style="color:orange;">**`craft_api`**</mark> <mark style="color:purple;">module is accessible.</mark>

{% code overflow="wrap" %}
```python
#!/usr/bin/env python

import pymysql
import sys
from craft_api import settings

# Test connection to MySQL database
connection = pymysql.connect(
    host=settings.MYSQL_DATABASE_HOST,
    user=settings.MYSQL_DATABASE_USER,
    password=settings.MYSQL_DATABASE_PASSWORD,
    db=settings.MYSQL_DATABASE_DB,
    cursorclass=pymysql.cursors.DictCursor
)

try:
    with connection.cursor() as cursor:
        sql = sys.argv[1]
        cursor.execute(sql)
        result = cursor.fetchall()
        print(result)
finally:
    connection.close()
```
{% endcode %}

#### <mark style="color:red;">`Example`</mark>

```sh
python myscript.py "SHOW GRANTS FOR CURRENT_USER()"
```
{% endhint %}

</details>
