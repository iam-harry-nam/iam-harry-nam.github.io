---
title: "How to convert List to an array in Kotlin?"
date: 2019-09-12 01:00:00
category: ["Kotlin"]
tag: ["How to convert List String to an String array in Kotlin",
      "how to put array value to vararg parameter to Java Function",
      "When will vararg needed"]
---

First, implement convert function
  
```kotlin
private inline fun <reified T> toArray(list: List<*>): Array<T> {
	return (list as List<T>).toTypedArray()
}
```
  
and then convert list to array with this function
  
```kotlin
val list:List<String> = lisfOf("harry", "potter")

val array = toArray<String>(list)
```
  
If you need to put array value to vararg parameter to Java Function, you need to put `*` front of variable
  
```kotlin
val familyName = getFamilyName(*array)
```
  

When will vararg needed? : when you need to import java library and a function which using vararg like below

  
```java
String familyName = getFamilyName(String... name);
```

