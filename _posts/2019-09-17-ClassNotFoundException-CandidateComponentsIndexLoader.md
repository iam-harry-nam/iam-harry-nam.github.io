---
title: "Caused by: ClassNotFoundException: CandidateComponentsIndexLoader"
date: 2019-09-17 01:00:00
category: ["Trouble Shooting"]
tag: ["Caused by: java.lang.NoClassDefFoundError: org/springframework/context/index/CandidateComponentsIndexLoader",
    "Caused by: java.lang.ClassNotFoundException: org.springframework.context.index.CandidateComponentsIndexLoader"]
---

_Trouble Shooting_

When I am using `implementation 'org.springframework.boot:spring-boot-starter-data-jpa'` library, 
and I get below error when project build.

```
Caused by: java.lang.NoClassDefFoundError: org/springframework/context/index/CandidateComponentsIndexLoader
	at org.springframework.orm.jpa.persistenceunit.DefaultPersistenceUnitManager.setResourceLoader(DefaultPersistenceUnitManager.java:431)
	at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.setResourceLoader(LocalContainerEntityManagerFactoryBean.java:320)
	at org.springframework.context.support.ApplicationContextAwareProcessor.invokeAwareInterfaces(ApplicationContextAwareProcessor.java:112)
	at org.springframework.context.support.ApplicationContextAwareProcessor.postProcessBeforeInitialization(ApplicationContextAwareProcessor.java:97)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.applyBeanPostProcessorsBeforeInitialization(AbstractAutowireCapableBeanFactory.java:416)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1691)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:573)
	... 63 more
Caused by: java.lang.ClassNotFoundException: org.springframework.context.index.CandidateComponentsIndexLoader
	at java.net.URLClassLoader.findClass(URLClassLoader.java:382)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:349)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	... 70 more
```

`org/springframework/context/index/CandidateComponentsIndexLoader` This class is not in project, so I searched this class and found this class is in latest `spring-context` library.

Here is document of this class, ["docs.spring.io/CandidateComponentsIndexLoader"](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/index/CandidateComponentsIndexLoader.html)

upgrade `spring-context` version from 4.x.x to 5.x.x

```groovy
dependency("org.springframework:spring-context:5.0.4.RELEASE")
```

