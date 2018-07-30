# spring-boot-mysql-caching_sha2_password-problem

If you need to use mysql 8+ in your application you should know that In MySQL 8.0, caching_sha2_password is the default authentication plugin rather than mysql_native_password. Some applications used to connect to this database will throw this exception:

Authentication plugin 'caching_sha2_password' cannot be loaded. how to resolve

Typical scenario:

You use docker trying to run mysql using mysql official image: (https://hub.docker.com/_/mysql/)

When I wrote this readme file 8.0.11 was latest version of mysql:

```
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:latest
```



If you use Spring boot version 2.0.0 (or older one) and use mysql-connector-java dependency:


![Spring boot connection problem](/boot_problem.png?raw=true "Spring boot connection problem")


If you use try to connect with mysql workbench:


![Mysql workbench problem](/mysql_workbench.png?raw=true "Mysql workbench problem")


The solution is very easy. You must connect to mysql and change the encryption of the user's password by altering the user with below Alter command (use old plugin) :

With docker open a terminal and connect to your container and change pasword of your user wuth old mysql_native_password:


```
docker exec -it mysql  bash     ()

mysql -u root -p (login as root )

// you need to change password to your user with mysql_native_password

ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root'; (use old mysql_native_password) (change root's password with old alternative)

```


**Link to youtube video demo:**

[![Video DEMO](/youtube-screen.png?raw=true)](https://youtu.be/vOUMmsHlMcY)


** This bug was fixed in Spring boot 2.0.3.release or later and it will be fixed inside mysql workbench MySql Workbench has a new version, that is compatible with MySQL 8.0. It is RC. **




