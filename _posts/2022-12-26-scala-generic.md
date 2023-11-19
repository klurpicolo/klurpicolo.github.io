---
layout: post
title:  "Scala Generic"
date:   2022-11-13 22:00:00 +0700
categories: [scala]
---

# Scala Generic
Scala type system support generic. Generic classes are classes that take a type(s) as parameter. For example, List[T], Seq[T], Option[T].

The following code will be used as an example for the rest of this article.
```scala
trait Animal

abstract class Mammal extends Animal {
  def name(): String
}
case class Dog(name: String) extends Mammal
case class Cat(name: String) extends Mammal

abstract class Fish
case class Salmon() extends Fish
case class Mackerel() extends Fish

//           Animal
//       |            |
//    Mammal         Fish
//   |       |     |      |
//  Dog     Cat  Salmon  Mackerel
```

# Upper bound and lower bound
Upper bound / Lower bound is the way to restrict that possible type that can be received.

## Systax
```scala
[T <: UpperBoundType] 
[T >: LowerBoundType]
[T <: UpperBoundType >: LowerBoundType]
```

- Upper bound : The way to limited type parameter. Let say, we want to write a method that take wrapper of mammal 
```scala
val dog = Dog("Tu")
val cat = Catog("Pom")

// the below method will cause complie error because it doesn't understand `name()` method that it exists. Therefore, we need to tell complier that `T` in this method will only `Mammal` or class below it.
def mammalSpeak[T](mammal: T): Unit = {
  println(mammal.name())
}

// to fix it, we need to add `Upperbound` => `<: Mammal`
def mammalSpeak[T <: Mammal](mammal: T): Unit = {
  println(mammal.name())
}
```
- Lower bound : Normally, we should not use lowerbound, except we develop library. Anyway, the logic is similar to upperbound but opposite instead. The type of lower bound is restrict that only accept the classes that are ancestor of the bounded type.

```scala
def classThatAreSuperOfDog[T >: Dog](wrapper: Wrapper[T]): Unit = {
  println(wrapper.toString)
}
```

# Covariant
Covariant is the concept that describe the relation of Generic classes regarding the type parameter. The reason that this exists is because that complier cannot assume the relation of `Wrapper` classes(List, Seq, Option, and so on). List[Dog] is not consider to be subtype of List[Animal] unless we specify that it is.

There are 3 type of relationship
- Covariance : This means the relation of `Wrapper` class is aligned the same way of its generic type
- Contravariance : This means the relation of `Wrapper` class is aligned the opposite way of its generic type
- Invariance : This is the default one which means there isn't relation at all.

Usecase 1
```scala
case class Wrapper[T](data: T) {
  def underlining(): T = data
}

val w1: Wrapper[Dog] = Wrapper(Dog("asd"))
val w2: Wrapper[Animal] = w1 //this cause complie error because Wrapper[Dog] isn't subtype of Wrapper[Animal]. We have to tell complier explicitly by add `Covariance` `+` sign to generic type

case class Wrapper[+T](data: T) {
  def underlining(): T = data
}
```

//TODO
Usecase 2
```scala

```