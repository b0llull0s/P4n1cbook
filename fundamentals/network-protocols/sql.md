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
{% code title="Default Port" %}
```
1433
```
{% endcode %}
{% endtab %}

{% tab title="MySQL" %}
{% code title="Default Port" %}
```
3306 and 33060
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

***

{% hint style="info" %}
## <mark style="color:orange;">`MySQL`</mark>

* <mark style="color:green;">**`MySQL Connector/Python`**</mark> <mark style="color:purple;">automatically appends a semicolon at the end of your queries.</mark>

***

### <mark style="color:purple;">Operator Precedence</mark>

<mark style="color:purple;">**Highest to lowest:**</mark>

1. <mark style="color:purple;">**Parentheses**</mark> <mark style="color:orange;">**`()`**</mark><mark style="color:purple;">: Operations inside parentheses are evaluated first.</mark>
2. <mark style="color:purple;">**Unary Operators**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">(highest precedence):</mark>
   * <mark style="color:orange;">**`+`**</mark> <mark style="color:purple;">(positive)</mark>
   * <mark style="color:orange;">**`-`**</mark> <mark style="color:purple;">(negation)</mark>
   * <mark style="color:orange;">**`~`**</mark> <mark style="color:purple;">(bitwise NOT)</mark>
   * <mark style="color:orange;">**`!`**</mark> <mark style="color:purple;">(logical NOT)</mark>
3. <mark style="color:purple;">**Multiplication, Division, Modulus**</mark><mark style="color:purple;">: These operators are evaluated next and have the same precedence:</mark>
   * <mark style="color:orange;">**`*`**</mark> <mark style="color:purple;">(multiplication)</mark>
   * <mark style="color:orange;">**`/`**</mark> <mark style="color:purple;">(division)</mark>
   * <mark style="color:orange;">**`%`**</mark> <mark style="color:purple;">(modulus)</mark>
4. <mark style="color:purple;">**Addition and Subtraction**</mark><mark style="color:purple;">: These operators have the next level of precedence:</mark>
   * <mark style="color:orange;">**`+`**</mark> <mark style="color:purple;">(addition)</mark>
   * <mark style="color:orange;">**`-`**</mark> <mark style="color:purple;">(subtraction)</mark>
5. <mark style="color:purple;">**Comparison Operators**</mark><mark style="color:purple;">: All of these operators have the same precedence:</mark>
   * <mark style="color:orange;">**`=`**</mark> <mark style="color:purple;">(equal to)</mark>
   * <mark style="color:orange;">**`!=`**</mark> <mark style="color:purple;">(not equal to)</mark>
   * <mark style="color:orange;">**`>`**</mark> <mark style="color:purple;">(greater than)</mark>
   * <mark style="color:orange;">**`<`**</mark> <mark style="color:purple;">(less than)</mark>
   * <mark style="color:orange;">**`>=`**</mark> <mark style="color:purple;">(greater than or equal to)</mark>
   * <mark style="color:orange;">**`<=`**</mark> <mark style="color:purple;">(less than or equal to)</mark>
   * <mark style="color:orange;">**`LIKE`**</mark> <mark style="color:purple;">(pattern matching)</mark>
6. <mark style="color:purple;">**Logical NOT**</mark><mark style="color:purple;">:</mark>
   * <mark style="color:orange;">**`!`**</mark> <mark style="color:purple;">(logical NOT)</mark>
7. <mark style="color:purple;">**Logical AND**</mark><mark style="color:purple;">:</mark>
   * <mark style="color:orange;">**`&&`**</mark> <mark style="color:purple;">(AND)</mark>
8. <mark style="color:purple;">**Logical OR**</mark><mark style="color:purple;">:</mark>
   * <mark style="color:orange;">**`||`**</mark> <mark style="color:purple;">(OR)</mark>

***

### <mark style="color:purple;">Commands</mark>

### <mark style="color:purple;">General</mark>

{% code title="Connect to the database" %}
```sh
mysql -u USER -h HOST -P PORT -p
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

#### <mark style="color:purple;">Tables</mark>

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

{% code title="Add values to table" %}
```sql
INSERT INTO table_name VALUES (value_1,..);
```
{% endcode %}

{% code title="Add values to column in a table" overflow="wrap" %}
```sql
INSERT INTO table_name(column2, ...) VALUES (column2_value, ..);
```
{% endcode %}

{% code title="Update table values" overflow="wrap" %}
```sql
UPDATE table_name SET column1=newvalue1, ... WHERE <condition>;
```
{% endcode %}

#### <mark style="color:purple;">Columns</mark>

{% code title="Show all columns in a table" %}
```sql
select * from table_name;
```
{% endcode %}

{% code title="Show columns from a table" %}
```sql
select name,username,password from sd4fg_users;
```
{% endcode %}

{% code title="Delete a table" %}
```sql
DROP TABLE tablename;
```
{% endcode %}

{% code title="Add a new column" overflow="wrap" %}
```sql
ALTER TABLE logins ADD newColumn INT;
```
{% endcode %}

{% code title="Rename column" overflow="wrap" %}
```sql
ALTER TABLE logins RENAME COLUMN newColumn TO oldColumn;
```
{% endcode %}

{% code title="Change column datatype" overflow="wrap" %}
```sql
ALTER TABLE logins MODIFY oldColumn DATE;
```
{% endcode %}

{% code title="Delete column" overflow="wrap" %}
```sql
ALTER TABLE logins DROP oldColumn;
```
{% endcode %}

#### <mark style="color:purple;">Output</mark>

{% code title="Sort By column" overflow="wrap" %}
```sql
SELECT * FROM logins ORDER BY column_1;
```
{% endcode %}

{% code title="Sort by column in descending order" overflow="wrap" %}
```sql
SELECT * FROM logins ORDER BY column_1 DESC;
```
{% endcode %}

{% code title="Sort by column in Ascending order" overflow="wrap" %}
```sql
SELECT * FROM logins ORDER BY column_1 DESC, id ASC;
```
{% endcode %}

{% code title="Sort by two-columns" overflow="wrap" %}
```sql
SELECT * FROM logins LIMIT 2;
```
{% endcode %}

{% code title="Only show first two results starting from index 2" overflow="wrap" %}
```sql
SELECT * FROM logins LIMIT 1, 2;
```
{% endcode %}

{% code title="List results that meet a condition" overflow="wrap" %}
```sql
SELECT * FROM table_name WHERE <condition>;
```
{% endcode %}

{% code title="List results where the name is similar to a given string" overflow="wrap" %}
```sql
SELECT * FROM logins WHERE username LIKE 'admin%';
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:orange;">`NoSQL`</mark>

### <mark style="color:orange;">`MongoDB`</mark>

#### <mark style="color:purple;">Commands</mark>

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
