---
layout: post
title:  "Scala 101"
date:   2022-08-13 22:00:00 +0700
categories: [scala]
---

# Scala
- Scala is a language that base on JVM
- Scala is functional language that inherit from Haskell
- Functions are first class citicen in Scala

# val, var, def, lazy val
- val : val is immutable data type, evaluates only once
- var : var is mutable 
- def : is method, evaluates every time it gets called
- lazy val : similar to val, but the value is evaluates once when the first access is called
```scala 
val immutable = 1 // similar to final in Java
val func1 = (a: Int, b: Int) => a+b // this is function
var mutable = "this can be changed"
def method1 = (a: Int, b: Int) => a+b //method
lazy val lazyVal = {
    println("init lazily")
    3
}
```

# Block
{} is combinded expressions the result of the last expression is the returned the block
```scala
{
    println("init val")
    5 // this is the return val P
}
``` 

# Object class
Object class is signlenton/static which there is only 1 instance on JVM.

# Companion object
Companion object is an object with the same name as class in the same file. It's used for store instance-indepedent field/method (static) related to the class. For example, we can put factory related method into Companion object.

# Case class
Case class is class that Scala help implement a lot of methods automatically(similar to record in Java)
- All parameters are val and public
- hashCode, equal, apply, unapply and so on
```scala
case class Person(name: String, age: Int)

val klur = Person("klur", 28) // don't need new because apply is automatically implemented
```

# Pattern matching
Pattern matching is the powerful feature that extends from simple switch case
```scala
val matcherFunc = (a: Int) => a match {
  case 1 => 1
  case 5 => "is five"
  case _ => "the rest"
}

//Pattern matching also work with case class
val klurSay = klur match {
      case Employee(name) => s"$name is just normal guy"
      case Boss(name, age) if age > 40 => s"$name is a old $age boss"
      case Boss(name, age) if age <= 40 => s"$name is a young $age boss"
    }
```

# Pattern guards
Pattern guards is a way to seperate the pattern matching by using if condition like the example above

# Extension methods and Implicit classes
Extension methods is the way to add method to an existing type or 3-party type which added in Scala3 which previously we can achive it by using Implicit classes
```scala
object StringExtensions {
    extension (str: String) {
      def toSnakeCase = {
        str.replaceAll("([A-Z])", "_" + "$1").toLowerCase
      }
    }
  }
```

# Try, Option
They are classes that wrap that actual underlining data. They are case class, so we can handle them using case matching. Another example is Future.onComplete() which take Try[T] => U as arguments.
Try -> Success or Exception
Option -> Some or None
```scala
val possibleException = Try(throw new RuntimeException("PANIC"))
val result = possibleException match {
  case Success(_) => "it success somehow"
  case Failure(exception) => s"error with ${exception.getMessage}"
}
println(result)
```

# For comprehensions
The form of it is ```for (enumerators) yield e```. They looks are equivalent to collection that concatinated using flatMap that produce as e in List.
```scala
val looping = for {
  x <- List(1,2)
  y <- List(3,4)
} yield (x,y)

looping.foreach((a: Int, b: Int) => println(s"$a and $b"))
//1 and 3
//1 and 4
//2 and 3
//2 and 4
```

# Currying
Curring is the process of converting a fucntion with multiple arguments into funtion with less argument(less generic).
```scala
def applyTo(operation: (Int, Int) => Int)(a: Int, b: Int): Int = {
  operation(a,b)
}

val plusOperation = (arg1: Int, arg2: Int) => arg1 + arg2
val plus: (Int, Int) => Int = applyTo(plusOperation)
println(plus(1,2)) // =3

val exponentialOperation = (arg1: Int, arg2: Int) => Math.pow(arg1,arg2).toInt
val exponential: (Int, Int) => Int = applyTo(exponentialOperation)
println(exponential(2,3)) // =8
```