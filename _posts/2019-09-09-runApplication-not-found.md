---
title: "runApplication not found"
date: 2019-09-09 01:00:00 -0700
category: ["Trouble Shooting"]
tag: ["runApplication","Spring Boot","Spring Boot 2","Spring Boot 1"]
---

_Trouble Shooting history_

I create new project with IntelliJ's spring initializer (link : _[https://start.spring.io/]_ )

<a href="/resource/image/20190909/springBoot_1.png"><img src="/resource/image/20190909/springBoot_1.png" width="700px" title="runApplication" /></a>

And main function is automatically generate, but runApplication does not configured because below can't import.

> import org.springframework.boot.runApplication

As a result, I had to **upgrade spring boot version from 1.x.x to 2.0.4.RELEASE** and problem solved.

[https://start.spring.io/]: https://start.spring.io/