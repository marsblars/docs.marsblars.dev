---
layout: post
title: "GAS Assembly MJC CSCI273 Final"
date: 2023-01-28 22:36:00 -0100
categories: [Academics,Finals]
tags: [asm,mjc,final]
---


## Final Prompt:
---

   
            
>  YOUR TURN 
>
> 1. Enter the program in Listing **10-5** and use gdb to single-step through the code. Notice that when you execute the `mov` `rsp`, `rbp` instruction in the epilogue, TUI does not highlight the registers. Explain. Next, change the program so that it returns the integer 123. Run it with `gdb`. What number base does `gdb` use to display the exit code?
>
> 2. Enter the program in Listing **10-1** and compile it with debugging turned on (`-g` option). Set a breakpoint at main. Does gdb break at the entry to the function? Can you follow the actions of the prologue by using the s command? Can you continue through the program and step through the epilogue?
>
> 3. Write the following C function in assembly language:
>
>
>```c
>/* f.c */
> int f(void) {
> return 0;
>}
>```
>
>
> 3. Make sure that it assembles with no errors. Use the `-S` option to compile `f.c` and compare gcc's assembly language with yours. Write a main function in C that tests your assembly language function, `f`, and prints out the function’s return value.
>
> 4. Write three assembly language functions that do nothing but return an integer. They should each return a >different, nonzero integer. Write a main function in C that tests your assembly language functions and prints >out the functions’ return values by using printf.
>
> 5. Write three assembly language functions that do nothing but return a character. Each should return a >different character. Write a main function in C that tests your assembly language functions and prints out the >functions’ return values by using `printf`.
> 
> Final based on Chapter 10 of Bob Plantz's free ebook: [Introduction to Computer Organization](https://bob.cs.sonoma.edu/my_book/IntroCompOrg_preview.pdf)

## Response:
 1. In order to highlight the registers you need to give gdb the command `layout regs` After setting the program to return 123, the program exits with `code 0173` instead of saying the program exited normally. The `rax` register is also labeled as `0x7b` instead of `0x0`


![image](https://pics.marsblars.dev/i/159f1d0d-03eb-49e2-bfb6-2577a00aafd3.jpg "gdb_output")


 

 2. gdb breaks at `return 0;`. using the `s` command you can step into the epilogue but not the prologue since the program  jumps straight to the breakpoint.


![image](https://pics.marsblars.dev/i/f89f5c8d-f045-447c-91a7-2b6152f0f9cf.jpg "gdb_output")


 3. When comparing my written assembler code(`f.s`) with the auto generated assembler code(`ff`), some of the things that stand out in the generated code is the `.LFEO:` section and also some code written in between the `f:` function that are all prefixed with `.cfi_` 




![image](https://pics.marsblars.dev/i/a5603de5-5be0-44c8-90f1-8a38bb909ac0.jpg ) 




 After writing the assembler function, I wrote a C function named `fcall.c` to call the assembler function and print its return value: 
```c
//fcall.c
#include <stdio.h
int f(void);

int main(void)
{
    printf("return code: %i\n", f());
    return 0;
}
```
```bash
as -o f.o f.s #compile assembler program
gcc fcall.c f.s -o fcall # compiles c program
./fcall #returns "return code: 0"
```

 4. In order to call three assembly functions to return a non-zero integer I first assembled each `.s` file with their `.o` object file. After they were assembled then I needed to include each header file where the functions were declared into my main c program and call each of them to print their return values. 

```c
//test_ints.c
#include <stdio.h
#include "twelve.h"
#include "four.h"
#include "twenty.h"
int main (void) {
    int return1;
    int return2;
    int return3;
    return1 = twelve();
    return2 = four();
    return3 = twenty();
    printf("The returned ints are:\n%i\n", return1);
    printf("%i\n", return2);
    printf("%i\n", return3);
    return 0;
}
```
After that all that was left was to compile the assembler files with the c program and to run it.
```bash
gcc test_ints.c twelve.s four.s twenty.s -o test_ints #compile c progam with assembly programs
./test_ints #returns:                    The returned ints are:
#                                        12
#                                        4
#                                        20
```

 5. Getting a C program to print the character returns of assembler functions was relatively similar to the previous example. There were still some important differences between the two however. First, in the main C program, the return values needed to be declared with `char` instead of `int`. Also when using `printf`, the statement needed to include `%c` instead of `%i` in order to specify the character was being returned. 

```c
//test_char.c 
#include <stdio.h
#include "a.h"
#include "b.h"
#include "c.h"
int main (void) {
    char return1;
    char return2;
    char return3;
    return1 = a();
    return2 = b();
    return3 = c();
    printf("The returned characters are:\n%c \n", return1);
    printf("%c \n", return2);
    printf("%c \n", return3);
    return 0;
}
```
 Next, the `.s` files needed the character return to be surrounded by quotes in order to specify that it is a string value.

```bash
#a.s
    .text
    .globl a
    .type a, @function

a:
    pushq %rbp                       
    movq  %rsp, %rbp                    
    movq  $'a', %rax                      
    movq  %rbp, %rsp                      
    popq  %rbp                            
    ret
```
 The final difference can be seen when compiling the C program with the `.s` files. The `gcc` command needed to include the `no-pie` flags in order to compile without errors.
```bash
gcc -fno-pie -no-pie test_char.c a.s b.s c.s -o test_char #compiles c program with asm functions
./test_char  #returns:             The returned characters are:
#                                  a
#                                  b
#                                  c
```