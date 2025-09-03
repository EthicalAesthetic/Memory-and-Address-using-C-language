# Learn Memory and Address using C language (16 bits)
This repository contains C programs that demonstrate how memory and addresses work in a 16-bit environment. The programs illustrate concepts such as pointers, memory allocation, and address manipulation.
## Table of Contents
- [1. Hexadecimal representation](#1-hexadecimal-representation)
- [2. Memory Cell in a computer](#2-memory-cell-in-a-computer)
- [3. Resident memory](#3-resident-memory)
    - [Physical address of computer](#physical-address-of-computer)
- [4. Segmentation of memory](#4-segmentation-of-memory)
    - [Offset address meaning](#offset-address-meaning)
    - [Data segments in c language](#data-segments-in-c-language)
        - [1. Stack area](#1-stack-area-)
        - [2. Data Area](#2-data-area)
        - [3. Heap area](#3-heap-area)
        - [4. Code area](#4-code-area)
- [5. Data types in c language](#5-data-types-in-c-language)




# 1. Hexadecimal representation

| Hexadecimal | Decimal | Binary  |
|-------------|---------|---------|
| 0           | 0       | 0000    |
| 1           | 1       | 0001    |
| 2           | 2       | 0010    |
| 3           | 3       | 0011    |
| 4           | 4       | 0100    |
| 5           | 5       | 0101    |
| 6           | 6       | 0110    |
| 7           | 7       | 0111    |
| 8           | 8       | 1000    |
| 9           | 9       | 1001    |
| A           | 10      | 1010    |
| B           | 11      | 1011    |
| C           | 12      | 1100    |
| D           | 13      | 1101    |
| E           | 14      | 1110    |
| F           | 15      | 1111    |

<br>
<img src="Resources/Screenshot 2025-09-03 163159.png">
<br><br>
<img src="Resources/Screenshot 2025-09-03 164224.png">
<br><br>
<img src="Resources/Screenshot 2025-09-03 164530.png">
<br><br>

# 2. Memory Cell in a computer
Entire RAM has divided in numbers of equal parts, which are  
known as memory cells. Following diagram represents the 256  
MB RAM.<br><br>
<img src="Resources/Screenshot 2025-09-03 165405.png">
<br><br>
Each cell can store one-byte data. Data are stored in the binary number system. 

That is a `character` data reserves `one` memory cell and `integer`data reservers `two` while `floating` data reserves `four` memory cells. Each memory cell has unique address. 

Address is always in whole number and must be in increasing order. We will discuss how a characters, integers etc. data are in stored in the data type chapter.

Just for now assume:-
```bash
int a = 4;
```
<img src="Resources/Screenshot 2025-09-03 171516.png">
If 0x5000 is the address of the memory cell where value 4 is stored. Address of next memory cell (?) will be 0x5001 and so on in increasing order.
<br><br>

# 3. Resident memory
Ram is diivided into two parts: 
- Resident memory 
- Extended memory (useless for now)

<img src="Resources/Screenshot 2025-09-03 172220.png">

Resident memory is the portion of a computer's memory that is currently being used by the operating system and active applications. It is the memory that is "resident" in the RAM (Random Access Memory) and is readily accessible for processing tasks.

When any program is executed it is stored in the residence memory. For turbo c 3.0, it has 1MB residence memory i.e. when we open turbo c 3.0 it stores 1MB in the RAM. 

## Physical address of computer  
All the c variables are stored in the residence memory. In turbo C 3.0, 20 bits address of the memory cell is known as physical address or real address. In 20 bits, we can represent address from 0x00000 to 0xFFFFF. That is all c variables must have memory address within this range.

<IMG src="Resources/Screenshot 2025-09-03 172919.png">
<br><br>
A C programmer cannot not decides what will be the memory address of any variables. It is decided by compiler. 

For Example: -

What will be output of following c code? 

```c
#include<stdio.h> 
int main(){ 
int a; 
printf("%x",&x); 
return 0; 
}

#apmersand(&) is used to get the address of variable.
``` 

<b>Output:</b> We cannot predict.

It may be 0x12345 or 0x54321 or any other address within 0x00000 to 0xFFFFF. 

But we can say in 16 bits compilers address must be within 0x0000 to 0xFFFF and in 32 bits compilers memory address must be within 0x00000000 to 0xFFFFFFFF.

<b>Note:</b> <i>Suppose your c compiler is based on the microprocessor which total address buses are 32 then its total size of addressable memory will be:</i>
<div align="center">

`Addressable Memory = 2 ^ (Number of Address Bus)`
</div>

= 2^32 bytes<br>
= 4GB

# 4. Segmentation of memory

Residential memory of RAM of size 1MB has divided into 16 equal parts. These parts is called segment.

Each segment has size is 64 KB. 

16 * 64 KB = 1 MB <br>
(2^4 * 2^6 * 2^10) bits = 2^20 bits = 1 MB<br><br>
<img src="Resources/Screenshot 2025-09-03 181254.png">

This process of dividing memory into segments is called segmentation of memory.

<b>NOTE:</b> In turbo c 3.0 physical addresses of any variables are stored in the 20 bits. But we have not any pointers (We will discuss later what is pointer?)of 
size 20 bits. <br>
So pointers cannot access whole residence memory address.To solve this problem we there are three types pointers in c language. They are:-

   1. Near pointer 
   2. Far pointer 
   3. Huge pointer

We will discuss these pointers in the pointer chapter.
## Offset address meaning 
Each segment has divided into 2 parts. They are:-
- Segment number (4 bit)
- Offset address (16 bit)
<br><br>
<img src="Resources/Screenshot 2025-09-03 231527.png">

### Example
Suppose physical address of any variable is 0x500F1.<br>
Then its segment number and offset address is:-
- Segment number = 5
- Offset address = 00F1

<b>Write a program to find the offset address of any variable</b>
```c
#include<stdio.h>
int main(){
    int x;
    printf("%u ",&x);  //To print offset address 
printf("%p ",x);      //To print segment address 
printf("%p ",&x);    //To print offset address 
printf("%fp ",&x);  //To print segment address : offset address 
return 0; 
}
```

## Data segments in c language (64 KB each)
<img src="Resources/Screenshot 2025-09-03 233008.png">

All the segments are used for specific purpose.<br>
We will discuss about how to access text video memory, graphics video memory in the pointer and union chapters of 255 bits color graphics programming.

## Data Segment (8th segment)
Segment number eight has special importance. It is called data segment. All the c variables are stored in this segment.

<b>This segment has been divided into four parts</b>.<br><br>
<img src = "Resources\Screenshot 2025-09-03 234156.png">

### 1. <u>Stack area </u>
All automatic variables and constants are stored into stack area. <br>Automatic variables and constants in c:-
1. All the local variables of default storage class. 
2. Variables of storage calls auto. 
3. Integer constants, character constants, string constants, float constants 
etc in any expression. 
4. Function parameters and function return values.

<br>
<b>NOTE:</b> Variables in the stack area are always deleted when program control reaches it out of scope. Due to this stack area is also called <i><b>temporary memory area</i></b>.

#### Example 1
What will be output of following c code? 
```c
#include<stdio.h> 
int main(){ 
int i; 
for(i=0;i<3;i++){ 
int a=5; 
printf("%d",a); 
} 
return 0; 
} 
```
<b>Output:</b>  5 5 5 

<b>Explanation:</b> Since variable `a` is automatic variable, it will store in the stack area. Scope of variable `a` is within for loop. So after each iteration variable a will be deleted from stack and in each iteration variable a will initialize. 

#### Example 2
What will be output of following c code? (Turbo C 3.0) (LIFO)
```c
#include<stdio.h> 
int main(){
    int a =5, b = 6, c = 7,d =8; 
printf("%d %d %d"); 
return 0; 
} 
```

<b>Output:</b> 8 7 6 

<b>Explanation:</b> Default storage class of variables a, b, c and d is auto .Since it automatic variable it will be sorted in the <i><b>stack</i></b> area of memory. It will store in the stack as
<div align="center">
<img src="Resources/Screenshot 2025-09-04 000716.png">
</div> 
Stack always follows LIFO data structure. In the printf function, name of 
variables is not written explicitly. So default output will content of stack 
which will be in the LIFO order i.e. 8 7 6.
<br><br>
<b>NOTE:</b> It has two part one for initialize variable another for non-initialize variable. All initialize variables are more nearer than non-initialized variable and vice versa. For example:-

#### Example 3
What will be output of following program? (Turbo c 3.0) (LIFO) 
```c
#include<stdio.h> 
int main(){ 
int a =5, b, c =7; 
printf("%d %d %d"); 
return 0; 
} 
```
<b>Output:</b> 7 5 garbage value 

<b>Explanation: </b> Automatic variable a and c has initialized while b has not initialized. 
Initialize variables are more nearer than uninitialized variable .They will be stored in the stack. So due to LIFO first output will be 7 then 5 (since a is more nearer than b with respect to c) then any garbage value will be 
output which is present in the stack. 

<b>NOTE:</b > Default storage class of any local variable is auto

### 2. <u>Data Area</u>
All the static variables and global variables are stored in the data area. It is permanent memory space and variable will store in the memory usless and until prgogram ends.

#### Example 1
What will be output of following c code? 
```c
#include<stdio.h> 
int main(){ 
int i; 
for(i=0;i<3;i++){ 
static int a=5; 
printf("%d",a); 
} 
return 0; 
} 
```
<b>Output:</b> 5 6 7 

<b>Explanation:</b> Since variable `a` is static variable, it will store in the data area. Scope of variable `a` is within for loop. So after each iteration variable a will not be deleted from data area and in each iteration value of variable a will be incremented by 1.

### 3. <u>Heap area</u>
This memory area is used for dynamic memory allocation. All the memory allocated by malloc(), calloc(), realloc() functions are stored in the heap area. It is also permanent memory space and variable will store in the memory unless and until prgogram ends. <i>It's size is not fixed. It depends on the size of residence memory.</i>

### 4. <u>Code area</u>
This memory area is used to store the executable code of the program. It is also permanent memory space and variable will store in the memory unless and until prgogram ends. <i>It's size is fixed for the fixed size of residence memory. (1MB in this case)</i>

## 5. Data types in c language
<img height="400px" src="Resources/Screenshot 2025-09-04 003451.png">