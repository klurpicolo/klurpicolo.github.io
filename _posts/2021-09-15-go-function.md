---
layout: post
title:  "Go fucntion"
date:   2021-09-15 21:00:00 +0700
categories: programming-language
tags: [go]
---

*Remark, I use term function for method in Java for simplicity.

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

