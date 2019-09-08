---
title: "runApplication not found"
date: 2019-09-09 01:00:00 -0700
category: ["Architecture","Back-End","Trouble Shooting"]
tag: ["can not import org.springframework.boot.runApplication",
     "org.springframework.boot.runApplication not found",
     "spring Boot Version 2.x.x"]
---

_Trouble Shooting history_

I create new project with IntelliJ's spring initializer (link : _[https://start.spring.io/]_ )

[##_Image|/resource/image/20190909/springBoot_1.png|alignCenter||runApplication_##]

And main function is automatically generate, but runApplication does not configured because below can't import.

> import org.springframework.boot.runApplication

As a result, I had to **upgrade spring boot version from 1.x.x to 2.0.4.RELEASE** and problem solved.

[https://start.spring.io/]: https://start.spring.io/