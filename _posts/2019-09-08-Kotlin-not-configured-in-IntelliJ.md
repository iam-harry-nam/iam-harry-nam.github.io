---
title: "Kotlin not configured in IntelliJ"
date: 2019-09-08 17:38:00 -0700
category: ["Trouble Shooting"]
tag: ["Kotlin not configured in IntelliJ",
     "add a dependency on the Kotlin standard library",
     "Kotlin version 1.3.41",
     "kotlin-gradle-plugin Kotlin-stdlib",
     "Spring boot create with Gradle by Kotlin"]
---

_Trouble Shooting history_

When I create spring-boot with Kotlin, IntelliJ can't reconize Kotlin class.

<a href="/resource/image/20190908/kotlin_1.png"><img src="/resource/image/20190908/kotlin_1.png" width="700px" title="Kotlin not configured message" /></a>

As a result, I added the standard library to dependency management.

<a href="/resource/image/20190908/kotlin_2.png"><img src="/resource/image/20190908/kotlin_2.png" width="700px" title="build.gradle" /></a>

> implementation("org.jetbrains.kotlin:kotlin-stdlib")

**Kotlin-stdlib** has extended versions of the standard library that add support for some of the features of JDK 7 and JDK 8.

Checking _[Kotlin language official page]_ this link and choose apropriate one.

[Kotlin language official page]: https://kotlinlang.org/docs/reference/using-gradle.html#configuring-dependencies
