---
title: "How to use cherry-pick?"
date: 2019-11-01 23:25:00
category: ["Git"]
tag: ["cherry-pick",
        "Git"]
---

Sometimes we want to migrate other developer's work to my branch.

In this case, there are two ways.

1) checkout to their branch and copy their code and checkout my branch and paste code..  
2) use git cherry-pick

I usually did like first way.. but I tried to use cherry-pick recently, and surprised it is **so Easy and Fast**

Here is summary to use cherry-pick!

```
$ git cherry-pick [ commit Hash-value ]
```

That's all!  
You don't need to complicated and time wasting step.

And here is tip. Git cound recognize 5 serial values of commit value.  
Here is example.

<a href="/resource/image/20191101/gitlog.png"><img src="/resource/image/20191101/gitlog.png" width="700px" title="git log" /></a>

```
$ git log
$ commit 463c9f00e4ea0833e9cbe9bdc04ea336a5ae1054 (HEAD -> master, origin/master, origin/HEAD)
$ Author: HarryNam <qpit2u@gmail.com>
$ Date:   Tue Oct 29 21:53:34 2019 +0900
$
$   new post How to calculate IQR and what is outlier detection
$
$ quit
$ git cherry-pick 463c9
```
