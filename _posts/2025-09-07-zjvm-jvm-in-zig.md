---
layout: post
title:  "Zjvm: Building a JVM in Zig"
date: 2025-07-20
---

I've built a toy [JVM in Zig](https://github.com/lyledean1/zjvm) as a way to dive deeper into understanding how the JVM works under the hood. Currently it supports a number of core features:
- Static methods and classes
- For loops and while loops
- If/else statements
- Classes with object creation and simple heap management


It can successfully compile and run this Java code:
```java 
public static void main(String[] args) {
    Printer printer = new Printer(0);
    
    int n = 10;
    printer.print("Fibonacci sequence:");
    
    for (int i = 0; i < n; i++) {
        printer.print(fibonacci(i));
    }
}

public static int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

Features I'd still like to add include:
- Simple garbage collection
- Native methods (currently mocked)
- Loading classes from libraries and JAR files

## Why Zig 

I've been learning Zig over the past year, and as someone who uses Rust quite frequently, I thought I'd branch out and try it for a larger project. I've really enjoyed working with it, especially with the improvements in Zig 0.15.

## Architecture


## Inspiration 

I found these resources about other toy JVM implementations in Java and Rust incredibly helpful, and I highly recommend checking them out:
- [I have written a JVM in Rust](https://andreabergia.com/blog/2023/07/i-have-written-a-jvm-in-rust/)
- [Implementing a Simple JVM in Java and Rust by Ben Evans](https://www.youtube.com/watch?v=KVxloQHRYvU&t=9s)