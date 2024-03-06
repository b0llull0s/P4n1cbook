# RDBMS

**MySQL**

* Create Database

```
sudo mysql -u root -p
```

```
create database cacti;
GRANT ALL ON cacti.* TO cacti@localhost IDENTIFIED BY 'cacti';
flush privileges;
exit
```

```
sudo mysql -u root -p mysql < /usr/share/mysql/mysql_test_data_timezone.sql
```

```
sudo mysql -u root -p
GRANT SELECT ON mysql.time_zone_name TO cacti@localhost;
flush privileges;
exit
```
