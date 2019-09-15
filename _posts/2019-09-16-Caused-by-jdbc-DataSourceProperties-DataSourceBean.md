---
title: "Main class name has not been configured and it could not be resolved"
date: 2019-09-16 01:00:00
category: ["Trouble Shooting"]
tag: ["contextLoads FAILED java.lang.IllegalStateException",
    "Caused by: org.springframework.boot.autoconfigure.jdbc.DataSourceProperties$DataSourceBeanCreationException"]
---

_Trouble Shooting_

I have created initial project and I get `java.lang.IllegalStateException`

```
Task :common-service:test FAILED

com.iamfullstack.common.CommonApplicationTests > contextLoads FAILED
    java.lang.IllegalStateException
        Caused by: org.springframework.beans.factory.UnsatisfiedDependencyException
            Caused by: org.springframework.beans.factory.BeanCreationException
                Caused by: org.springframework.beans.BeanInstantiationException
                    Caused by: org.springframework.boot.autoconfigure.jdbc.DataSourceProperties$DataSourceBeanCreationException

1 test completed, 1 failed
```
  

The problem was that I was import RDB related library
```groovy
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
```
and I have to set SQL connection properties.

  
```properties
spring.datasource.url=jdbc:mysql://localhost/database
spring.datasource.username=username
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```
  

Another option is, removing import library `spring-boot-starter-data-jpa` from gradle.