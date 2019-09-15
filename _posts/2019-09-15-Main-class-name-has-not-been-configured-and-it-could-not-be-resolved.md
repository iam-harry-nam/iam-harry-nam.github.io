---
title: "Main class name has not been configured and it could not be resolved"
date: 2019-09-15 01:00:00
category: ["Trouble Shooting"]
tag: ["Execution failed for task ':bootJar'. Main class name has not been configured and it could not be resolved",
      "bootJar.enabled = false"]
---

This error happens on bootJar job.

```
Execution failed for task ':bootJar'.
> Main class name has not been configured and it could not be resolved
```


This is because there is no main class in DAO package. (in My case)



In my case, just add one line in dao/build.gradle, and fixed. 


```groovy
bootJar.enabled = false
```


But, if there is exist main class, just set main class in build.gradle like


```groovy
bootJar {
    mainClassName = 'org.syaku.blog.Application'
}
```


