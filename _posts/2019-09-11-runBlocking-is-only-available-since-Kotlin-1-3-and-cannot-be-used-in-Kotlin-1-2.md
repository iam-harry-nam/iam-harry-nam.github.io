---
title: "runBlocking(CoroutineContext = ..., suspend CoroutineScope.() -> T): T is only available since Kotlin 1.3 and cannot be used in Kotlin 1.2"
date: 2019-09-11 01:00:00
category: ["Trouble Shooting"]
tag: ["runBlocking(CoroutineContext = ... suspend CoroutineScope.() -> T): T is only available since Kotlin 1.3 and cannot be used in Kotlin 1.2",
      "CoroutineContext version up issue",
      "having trouble when kotlin version upgrade",
      "kotlin version management in build gradle",
      "runBlocking CoroutineContext CoroutineScope"]
---

I was using Kotlin version 1.2.41 and I upgraded Kotlin version 1.2.41 to 1.3.21. Then, I got compile Error. 

> ‘runBlocking(CoroutineContext = ..., suspend CoroutineScope.() -> T): T’ is only available since Kotlin 1.3 and cannot be used in Kotlin 1.2

Here is original code

```groovy
plugins {
    id "org.jetbrains.kotlin.jvm" version "$kotlinVersion"
    id "org.jetbrains.kotlin.plugin.spring" version "$kotlinVersion"
    id "nebula.kotin" version "1.2.41"
}

compileKotlin {
    kotlinOptions {
        apiVersion = "1.2"
        languageVersion = "1.2"
    }
}

org.jetbrains.kotlin:kotlin-stdlib-jdk8:$kotlinVersion
org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlinVersion
org.jetbrains.kotlin:kotlin-stdlib:$kotlinVersion
org.jetbrains.kotlin:kotlin-reflect:$kotlinVersion


org.jetbrains.kotlinx:kotlinx-coroutines-core:$kotlinStdlib
org.jetbrains.kotlinx:kotlinx-coroutines-jdk8:$kotlinStdlib
org.jetbrains.kotlinx:kotlinx-coroutines-nio:$kotlinStdlib
org.jetbrains.kotlinx:kotlinx-coroutines-rx2:$kotlinStdlib
org.jetbrains.kotlinx:kotlinx-coroutines-reactor:$kotlinStdlib
```

and I changed these variables from 
```groovy
kotlinStdlib = 1.2.31
kotlinVersion = 1.2.41
kotlinxCoroutines = 0.22.5
```

to 

```groovy
kotlinStdlib = 1.3.21
kotlinVersion = 1.3.21
kotlinxCoroutines = 1.2.2
```

But I get error on `kotlinx.coroutines.runBlocking` function as below

> ‘runBlocking(CoroutineContext = ..., suspend CoroutineScope.() -> T): T’ is only available since Kotlin 1.3 and cannot be used in Kotlin 1.2

I solved problem with below steps.

First, I searched google but there was so old reference come up : [https://stackoverflow.com/questions/53030756/launch-is-only-available-since-kotlin-1-3-and-cannot-be-used-in-kotlin-1-2](https://stackoverflow.com/questions/53030756/launch-is-only-available-since-kotlin-1-3-and-cannot-be-used-in-kotlin-1-2)

I followed above reference(try this first since it might possible to fix your case): 
**checking IDEA Setting**(Kotlin Compiler version, Kotlin plugin version) 

But it doesn't help for me.

Finally, I found that **one of library(nebula.kotlin) is using kotlin** which version is legacy(1.2.41) -> need to change 1.3.21

And also **apiVersion, languageVersion** in **kotlinOptions** in Build.gradle file, is also pointing Kotlin version 1.2.x. -> need to 1.3 or remove

and then finally fixed, go to bed
