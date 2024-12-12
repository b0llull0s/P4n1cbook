---
icon: server
---

# MySQL

{% hint style="info" %}
## <mark style="color:purple;">Default Ports:</mark> <mark style="color:orange;">`3306`</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">`33060`</mark>

* <mark style="color:purple;">Use</mark> <mark style="color:orange;">**`ss -tlpn`**</mark> <mark style="color:purple;">**to check if is being run locally.**</mark>

### <mark style="color:green;">`Python`</mark> <mark style="color:purple;">-></mark> <mark style="color:green;">`MySQL Connector/Python`</mark> <mark style="color:purple;">automatically appends a semicolon at the end of your queries.</mark>
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:orange;">`MySQL`</mark> <mark style="color:purple;">Operator Precedence</mark>

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
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">Commands:</mark>

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

