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




If you use try to connect with mysql workbench:







