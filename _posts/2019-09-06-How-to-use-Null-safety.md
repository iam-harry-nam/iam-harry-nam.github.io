---
title: "How to use Null safety"
date: 2019-09-06 11:13:00 -0700
category: ["Computer Language", "Kotlin"]
tag: ["NullPointerException Java Kotlin", "NullPointerException billion dollar mistake"]
---


One of the most common errors in many programming languages, including Java, is that accessing a member without a reference value results in a null reference exception. In Java, this is equivalent to **NullPointerException** or **NPE**.

`Tony Hoare` who applied NPE first time said.

> "I call it my billion-dollar mistake."

Kotlin is basically developed to not allow nulls when defining variables, and even if it allows nulls, it has the advantage of being able to safely develop by checking the possibility of referencing nulls at compile time. (The biggest advantage I think)




## Non-Nullable Variables vs. Nullable Variables

```kotlin
fun test(a: String, b: String?) {
    // Do noting
}
```

You can clearly see the difference in the following code: It's simple. `?` is the difference.

If `?` is added, it means that this can also refer to Null. 

If `?` doesn't exist, it means the variable that doesn't have a null reference.

```java
String name = null;
int size = -1;

if (name != null) {
  size = name.length();
}
```

Null check in Java like this

```kotlin
var name: String? = null
val size = name?.length ?: 0
```


In Kotlin you can abbreviate this.
`?` usage will explain below.


## Safe Calls
In Kotlin, when you need to check null and call only if it is not null, you can add `?.` to nullable variable.

This is Safe Calls!


```kotlin
// Nullable variable
val name: String? = null
// You can avoid calling length from a null object if you use ?.
val size = name?.length
```


In the above result, `name` is null, so length function is not called and `size` contains Null.

This advantage can be used to simplify code when referencing internal variables within nested classes.

In Java, there are a lot of people who have experienced this. In the real world, business is complicated and these cases are frequent.
```java
// null check
if (school != null && school.class != null && school.class.name != null) {
	return school.class.name.age;
}

return null;
```

In Kotlin, on the other hand, you can knit in one line.

```kotlin
// safe calls chaining
return school?.class?.name?.age
```


## And you can throw an exception if you refer to a null reference

There are some variables are obviously not nullable, but some cases where you must declare Null variables. I use it mainly when API calls and handling response messages are not Null in API response messages. 

In Kotlin, using !! produce NPE if it is null and then calls function.

```kotlin
var name: String? = null
val size = name!!.length
```

This code will happen NullPointerException


## Avoid errors that can occur when casting

In Kotlin, you can avoid TypeCaseException if you use `?` in your code.

```kotlin
val itemId: String? = ""

// TypeCastException happens
val itemIdAsInt: Int? = itemId.toInt

// This case TypeCastException not happens, save Null
val itemIdAsInt: Int? = itemId as? Int

// save 0, not Null
val itemIdAsInt: Int? = itemId as? Int ?: 0
```


## Using filterNotNull, filter Null element

If you use List containing Null element, code will long and unefficient by checking Null check. In that case, you can create Not Nullable type List so that you can easily develop with the list.

```kotlin
val nullContainList: List<Int?> = listOf(1, 2, null, 4)

for (i in nullableList) {
	// If you declare it as a nullable variable, you should develop it with null in mind whenever you use that variable like below
	nullContainList?.let {print("${i}")
}


// If you declare it as a non-null variable Int List as below, you don't have to worry about Null.
val intList: List<Int> = nullableList.filterNotNull()

for (i in intList) {
	print("${i} ")
}
```

In this way, Kotlin can prevent NPE by using non-null variables by default, and can safely and consequently check nulls even if it uses Null-reference variables.

**Kotlin** is a good language to prevent NPE.

