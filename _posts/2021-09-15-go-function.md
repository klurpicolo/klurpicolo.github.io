---
layout: post
title:  "Go fucntion101"
date:   2021-09-15 21:00:00 +0700
categories: programming-language
tags: [go]
---

*Remark, I use term function for method in Java for simplicity.

# Go function syntax
I've experience in Java and try to learn Go. Then first thing that makes me confuse in go is function syntax structure.

### Arguments
- Java : type then parameter name (int a)
- GO :  parameter name then parameter (a int)

### Return value
- Java : return value is placed in front of function name. Java only allows 1 only return value
- Go : return values is placed after function's arguments. Go allows to return multiple values

### Exception
- Java : multiple throw exceptions is declare after function arguments
- Go : in Go they call error instead and it can return as part of return values

Java example
```java
public float divideBy(int a, int b) throws Exception {
  if (b == 0) {
    throw new IllegalArgumentException("divider should not be 0");
  }
  return (float) a / (float) b;
}
```

Go example
```go
func divideBy(a, b int) (float32, error) {
	if b == 0 {
		return 0, errors.New("divider should not be 0")
	}
	return float32(a) / float32(b), nil
}
```

# Go pass value/pointer and value/pointer receiver
- In Go, They data always pass by value (copy into function).
- Object that pass in function will be copied into function, so changes in function will not effect object in the caller scope.
- in Java, method isn't first class citizen(It cannot exists without class). In contrast, function is first class citizen.
- Method in Java is attached to object since it's always under class. Go can achieve the same thing using **Receiver**

```go
package main

import (
	"fmt"
)

type person struct {
	name string
	age  int
}

func main() {

	person1 := &person{name: "klur", age: 27}

	fmt.Println("before all : ", person1)
	addAgeFunc(*person1, 10) // -- (1)
	fmt.Println("after added uning function", person1)
	addAgeFuncPnt(person1, 10) // -- (2)
	fmt.Println("after added uning function with pointer", person1)
	person1.addAgeReceiver(10) // -- (3)
	fmt.Println("after added uning function with receiver", person1)
	person1.addAgePntReceiver(10) // -- (4)
	fmt.Println("after added uning function with pointer receiver", person1)

}

//(1)
func addAgeFunc(p person, i int) {
	p.age += i
}

//(2)
func addAgeFuncPnt(p *person, i int) {
	p.age += i
}

//(3)
func (p person) addAgeReceiver(i int) {
	p.age += i
}

//(4)
func (p *person) addAgePntReceiver(i int) {
	p.age += i
}

```

## (1) -- Pass copy of value into function
This way the person object inside function is another obecjt than original one, so that chaging values inside function won't affect the original object as line 18 shown

## (2) -- Pass pointer of object into function
This way function get the pointer that references the original object, so that changing values inside function will effect that original object as line 20 showm

## (3) -- Function with value receiver
This way function is attached to object, so we can call from object following by dot. Moreover, the person value is stil just a copy of original object. So changes still not affect the original

## (4) -- Function with pointer receiver
Beside able to call from object following by dot. This pass as pointe, so changing values will affect the original. This is equivalent to Java's method.
