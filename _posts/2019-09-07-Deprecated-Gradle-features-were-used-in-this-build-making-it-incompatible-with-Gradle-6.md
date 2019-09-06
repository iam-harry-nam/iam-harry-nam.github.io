---
title: "Deprecated Gradle features were used in this build, making it incompatible with Gradle 6.0."
date: 2019-09-07 01:00:00 -0700
category: ["Architecture","Back-End","Trouble Shooting"]
tag: ["Deprecated Gradle features were used in this build making it incompatible with Gradle 6.0.",
     "Kotlin gradle plugin 1.3.20",
     "Kotlin version 1.3.20",
     "The DefaultSourceDirectorySet constructor has been deprecated.",
     "This is scheduled to be removed in Gradle 6.0.",
     "Please use the ObjectFactory service to create instances of SourceDirectorySet instead."]
---

When I run gradle, I got below message.

> Deprecated Gradle features were used in this build, making it incompatible with Gradle 6.0.

So, first I put `--warning-mode=all` to gradle command like below.

> ./gradlew clean build --warning-mode=all

And I find `DefaultSourceDirectorySet` class's constructor has been deprecated (below detail message)

> Configure project :  
> The DefaultSourceDirectorySet constructor has been deprecated. This is scheduled to be removed in Gradle 6.0. Please use the ObjectFactory service to create instances of SourceDirectorySet instead.

Kotlin 1.3.20 was released and also updated in the _[Gradle repository]_

**so this issue should be solved by updating the Kotlin Gradle plugin to 1.3.20.**

[Gradle repository]: https://plugins.gradle.org/plugin/org.jetbrains.kotlin.jvm
