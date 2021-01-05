---
layout: post
author: Chaz Lee
title: Kotlin Base Operations
date: 2020-08-21T11:47:20.613Z
thumbnail: /assets/img/posts/hello.jpg
categories: Tutorial
summary: knowledge summary
---
#####  __For loop[refer link](https://www.runoob.com/kotlin/kotlin-loop-control.html)__

Normal for loop：
```kotlin
for (i in 1..4) print(i) // print result: "1234"
```
Use downTo() to reverse intergers 
```kotlin
for (i in 4 downTo 1) print(i) // print result: "4321"
```
Specify step：
```kotlin
for (i in 1..4 step 2) print(i) // print result: "13"

for (i in 4 downTo 1 step 2) print(i) // print result: "42"
```
Use until() to iterate without boundary value
```kotlin
for (i in 1 until 10) { // i in [1, 10), not including 10
     println(i)
}
```

#####  __class Object__
```kotlin
class Runoob  constructor(name: String) {  // 类名为 Runoob
    // Inside {} is constructor
    var url: String = "http://www.runoob.com"
    var country: String = "CN"
    var siteName = name

    init {
        println("Initial Website Name: ${name}")
    }

    fun printTest() {
        println("This is function of class")
    }
}

fun main(args: Array<String>) {
    val runoob =  Runoob("Tutorial")
    println(runoob.siteName)
    println(runoob.url)
    println(runoob.country)
    runoob.printTest()
}
```
```kotlin
class Person {

    var lastName: String = "zhang"
        get() = field.toUpperCase() // Uppercase
        set

    var no: Int = 100
        get() = field              // value of field
        set(value) {
            if (value < 10) {      // return value if value < 10
                field = value
            } else {
                field = -1         // return -1 if value >= 10
            }
        }

    var heiht: Float = 145.4f
        private set
}

// Test main class
fun main(args: Array<String>) {
    var person: Person = Person()

    person.lastName = "wang"

    println("lastName:${person.lastName}")

    person.no = 9
    println("no:${person.no}")

    person.no = 20
    println("no:${person.no}")

}
