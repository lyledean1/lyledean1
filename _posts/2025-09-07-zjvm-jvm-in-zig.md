---
layout: post
title:  "zjvm: Building a JVM in Zig"
date: 2025-09-07
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

The implementation starts by loading all classes from the provided folder:

```bash
zig build run -- example/src/main/java/basic Fibonacci
```

This command loads all .class files in the "basic" folder, then executes the "main" method of the Fibonacci class. The first step is illustrated below. See the code [here](https://github.com/lyledean1/zjvm/blob/8b203b6bcc5300aa1496c9c78f96c0c22155d484/src/main.zig#L45)

<img width="338" height="524" alt="Screenshot 2025-09-07 at 16 14 20" src="https://github.com/user-attachments/assets/b7cd9309-08d0-40c2-8c73-611e921768d7" />

The classes are then stored in the Klass Repo, which the VM loop uses to find classes when executing invokestatic, invokevirtual, or invokespecial bytecodes. It looks up the appropriate class and method based on whether the call is static or instance-based. For instance methods, an object is created in the heap containing the instance fields for that class (this happens after the new instruction executes). Currently there's no garbage collector for the heap - that's another feature I plan to implement. The VM execute method is [here](https://github.com/lyledean1/zjvm/blob/8b203b6bcc5300aa1496c9c78f96c0c22155d484/src/runtime/vm.zig#L20)

<img width="638" height="600" alt="Screenshot 2025-09-07 at 16 40 27" src="https://github.com/user-attachments/assets/66785e9f-945f-4713-b1a3-afb096825911" />




## Inspiration 

I found these resources about other toy JVM implementations in Java and Rust incredibly helpful and inspiring, and I highly recommend checking them out:
- [I have written a JVM in Rust](https://andreabergia.com/blog/2023/07/i-have-written-a-jvm-in-rust/)
- [Implementing a Simple JVM in Java and Rust by Ben Evans](https://www.youtube.com/watch?v=KVxloQHRYvU&t=9s)
