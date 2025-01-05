---
layout: post
title:  "Hello World and Happy New Year!"
date: 2025-01-01
---

Hello World! I am going to attempt to blog a bit more this year, I've got quite a few topics to talk about around Compilers and Mobile development that I've been up to in my spare time. 

Today is the first day of 2025 - if you compile this machine code via gcc on ARM (MacOS) - It should output "Happy new year!" in your terminal.  

After saving the code below as "happy_new_year.s" - run 
```
gcc happy_new_year.s -o happy_new_year
./happy_new_year
```

(Generated after a bit of back and forth with [Claude.ai](https://claude.ai/))

```armasm
.global _main
.align 2

.data
message:
    .asciz "Happy New Year!\n"

.text
_main:
    stp     x29, x30, [sp, -16]!
    mov     x29, sp                   
    
    // Set up arguments for printf
    adrp    x0, message@PAGE          // Get the page address of message
    add     x0, x0, message@PAGEOFF   // Add offset within the page
    bl      _printf                   // Call printf
    
    // Return 0
    mov     w0, #0
    ldp     x29, x30, [sp], 16       // Restore frame pointer and link register
    ret
```
