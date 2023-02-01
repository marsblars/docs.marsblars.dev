---
layout: post
title: "Hello World 🎉️" 
date: 2023-01-27 14:47:00 -0500
categories: [Hello World]
tags: [basic]
---


**Hello World**

```c
#include <stdio.h>

int main() {
printf("Hello World");
return 0;
}
```

```c++
#include <iostream>

int main() {
	std::cout << "Hello World";
	return 0;
}
```

```c#
namespace HelloWorld
{
	class Hello {
		static void Main(string[] args)
		{
			System.Console.WriteLine("Hello World");
		}
	}
}
```

```python
print("Hello World")
```

```c 
/*assembly*/

    global _main
    extern _printf

    section .text
_main:
    push    message
    call    _printf
    add        esp, 4
message:
    db    'Hello World', 10, 0
```

```java
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
	public static void main (String[] args) {
	System.out.println("Hello World");
	}
}
```

```javascript
console.log("Hello World");
```

```bash
echo "Hello World"
```

```rust
fn main() {
    // Statements here are executed when the compiled binary is called

    // Print text to the console
    println!("Hello World!");
}
```
