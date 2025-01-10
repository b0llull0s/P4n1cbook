---
icon: database
---

# NoSQL

{% hint style="info" %}
## <mark style="color:orange;">`NoSQL`</mark>

### <mark style="color:red;">`MongoDB`</mark>

#### <mark style="color:purple;">`Commands`</mark>

{% code title="Start it" %}
```sh
mongo
```
{% endcode %}

{% code title="Show databases" %}
```mongodb
show dbs
```
{% endcode %}

{% code title="Select a database" %}
```mongodb
use database
```
{% endcode %}

{% code title="List tables (collections)" %}
```mongodb
show collections
```
{% endcode %}

{% code title="Show content from a collection (table)" %}
```mongodb
db.<collection>.find().pretty()
```
{% endcode %}

{% code title="Passing parameters (greater than/equal)" %}
```mongodb
db.<collection>.find({ age: { $gte: 18 } })
```
{% endcode %}

{% code title="Limit results (first five)" %}
```mongodb
db.users.find().limit(5)
```
{% endcode %}

{% code title="Dump a database" %}
```sh
mongodump --db <database_name> --out <backup_directory>
```
{% endcode %}

{% code title="Dump a collection" %}
```sh
mongodump --db myDatabase --collection myCollection --out /path/to/backup/
codeshe
```
{% endcode %}

* <mark style="color:orange;">**`Mongo`**</mark> <mark style="color:purple;">dump the data in binary form, creating</mark> <mark style="color:orange;">**`BSON`**</mark> <mark style="color:purple;">files, in order to convert then is a readable form use:</mark>

```sh
bsondump <input_bson_file>
```

* <mark style="color:purple;">It's possible also to restore a database from a dump file with:</mark>

```sh
mongorestore --db <database_name> <path_to_backup>
```
{% endhint %}

