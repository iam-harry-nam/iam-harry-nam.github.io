---
title: "Gradle Caching and Builds"
date: 2019-09-14 03:00:00
category: ["Gradle"]
tag: ["global caching task caching",
      "How to Cache clean up",
      "incremental build support UP-TO-DATE",
      "Remote Build Cache"]
---

Roughly Gradle does two kinds of caching: **global caching** for all projects and **task caching** on per project basis.

## Global Caching  

By default Gradle stores it in a home directory for a user.  
Path is `~/.gradle/caches`.

- `~/.gradle/caches/jars-3` and `~/.gradle/caches/$GRADLE_VERSION` contain jars needed for launching Gradle itself and to start execution of a build.  
- `~/.gradle/caches/transforms-1` contains transformed dependencies from all DependencyHandlers.  
- `~/.gradle/caches/modules-2` contains all the actual jar files and other metadata for all external dependencies of all projects that Gradle ever resolved on the current machine.

In order to clean up `~/.gradle/caches` folder we need:

- delete all \*.lock files that Gradle workers created for synchronized access to the caches.  
- delete ~/.gradle/caches/$GRADLE\_VERSION because it contains caches of file timestamps which change on every CI build.

How to Cach clean up with Terminal, just type like below!

```
$ rm -rf ~/.gradle/caches/$GRADLE_VERSION{put your Gradle version}/
$ find ~/.gradle/caches/ -name "*.lock" -type f -delete
```

## Task Caching

Gradle introduced _incremental build support_ aka `UP-TO-DATE` checks. The idea of UP-TO-DATE checks is pretty simple: If a task (1) has a known set of inputs and outputs and (2) does not have side effects then **inputs deterministically define outputs and task execution can be skipped if inputs hasn’t changed** from the previous build.

Gradle 3.5 took this idea to a completely different level. Before, 'UP-TO-DATE' checks worked only between sequential local invocations of Gradle which was a huge pain-point for people using feature branches in Git. Switching branches most likely was resulting in all `UP-TO-DATE` checks to fail on the next build. 

The build cache on the other hand allowed `UP-TO-DATE` checks to persist information about inputs and outputs not only between sequential invocations.

To enable the build cache for your Gradle project simply put `org.gradle.caching=true` in your `gradle.properties` file. By default Gradle stores Build Cache locally in `~/.gradle/caches/build-cache-1` folder which means it will be automatically cached in CI as we discussed above. 

**But it’s not that simple!** Build Cache size will grow overtime and by default it can be up to 5 GB. It’s quite a lot! 

In Gradle 4.6 Build Cache will switch to time based cache eviction policy which means everything that was unused in the last 7 days will be evicted from the cache. But still **Build Cache will contain a lot of artifacts that are not required for every build!**

Thankfully, there is an option to use a **Remote Build Cache.** Instead of storing everything locally Gradle will use a remote storage and download cached build artifacts only when they are needed.

Both _Gradle Enterprise_ and _Cirrus CI_ have built-in HTTP Build Cache and it’s very easy to setup. Here is an example of how to change `settings.gradle` file to setup HTTP Build Cache for _Cirrus CI_:

```groovy
ext.isCiServer = System.getenv().containsKey("CI") ext.isMasterBranch = System.getenv()["CIRRUS_BRANCH"] == "master" 
ext.buildCacheHost = System.getenv().getOrDefault("CIRRUS_HTTP_CACHE_HOST", "localhost:12321")
buildCache {   
  local {     
    enabled = !isCiServer   
  }   
  remote(HttpBuildCache) {     
    url = "http://" + buildCacheHost + "/"  
    enabled = isCiServer     
    push = isMasterBranch   
  } 
}
```

You can use the same configuration with Gradle Enterprise by simply changing `buildCacheHost` to point to your Gradle Enterprise instance.

_This is Summary of [Mastering-gradle-caching-and-incremental-builds](https://medium.com/cirruslabs/mastering-gradle-caching-and-incremental-builds-37eb1af7fcde)_

