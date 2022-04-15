---
attachments: [Clipboard_2022-04-14-18-17-08.png, Clipboard_2022-04-14-18-17-54.png]
tags: ['2011']
title: Assembly Guide
created: '2022-04-14T19:27:41.907Z'
modified: '2022-04-14T23:49:50.080Z'
---

# Assembly Guide
## General Info
rdi - first param
rsi - second param
rdx - third param
rax - result

b = byte = 8 bits **char**
w = word = 16 bits **short**
l = long = 32 bits **int** or 64 bits **float** paired with e registers
q = quad = 64 bits **long** or **char*** paired with r registers
```
INSTRUCTION SOURCE, DESTINATION # COMMENT
```
$ - a value
% - register / address

### Address Manipulation
parentheses are similar to pointer dereference
%rdi gives address
(%rdi) gives value of %rdi
treat registers are sort of like variables
#### p = 0x1234068 and *p = 10, then %rdi = 0x1234068 and (%rdi) = 10
val(add,reg,mult) = reg*mult + add + val
0x28(rdx, rsi, 8) = rsi*8 + rdx + 0x28

### Flags (single bit registers)
t is result of comparison
CF - unsigned overflow occurs
ZF - t == 0
SF - T < 0 (signed)
OF - two's compliment overflow occurs

### Compiler Options
gcc -Og -S -fno-if-conversion main.c

## Instructions
Cheat Sheet [^2]
mov - move value to register
```
movl $6, %eax # eax = 6
movw %eax, value # value = eax
```
lea - load effective address, stores calculated memory address in register
```
lea [ebx*2], ebx # multiply ebx by 2
```
cmp - compares two values, and stores the result in a flag
```
cmp %rdi, %rsi # effectively rsi - rdi, stores result
```
j - jump to specified location [^1] more jumps
```
jle loc # jump to loc
```
sh - shift (shr: shift right, shl: shift left)
ret - return value
```
ret %eax # returns eax
```

### Computation Instructions
add
sub
mul, imul (signed)

and
or
xor
not

## Control Loops
### Do While
<table>
<tr><th>C Code</th><th>Simplified</th><th>Assembly</th></tr>
<tr>
<td>

```c
do {
  // body
} while(x);
```
</td>
<td>

```c
loop:
  // body
  if(x) goto loop;
```
</td>
<td>

```py
.L2:
  # body
  jne .L2 # if(x) != 0
```
</td>
</tr></td></table>

Does the body, then tests. If test pases, jump back to body.

### While
<table>
<tr><th>C Code</th><th>Simplified</th><th>Assembly</th></tr>
<tr>
<td>

```c
while(x){
  //body
}
```
</td>
<td>

```c
goto test; // test before body
loop:
  // body
test:
  if(x) goto loop;
done:
```
</td>
<td>

```py
.test
  je .done
.L2:
  # body
  jne .L2 # if(x) != 0
.done
  ret
```
</td>
</tr></td></table>

Similar to do while, but has an initial test conditional. May be a goto test, or test, go to done.
With some optimization, translates to a do while, but negates the test.
`if(!test)`

### For
<table>
<tr><th>C Code</th><th>Simplified</th><th>Assembly</th></tr>
<tr>
<td>

```c
for(init; test; update){
  //body
}
```
</td>
<td>

```c
init;
loop:
{
  // body
}
update;
test goto loop;
```
</td>
<td>

```
  movl &0, %edx
.L2:
  # body
  addl &1, %edx
  cmp %edx, 10 # test
  jne .L2
.done
  ret
```
</td>
</tr></td></table>

For loop basically gets translated to while loop
No need for initial test like while loop, since the value is initialized to pass the loop in the first place.

### Switch
<table>
<tr><th>C Code</th><th>Simplified</th><th>Assembly</th></tr>
<tr>
<td>

```c
switch(x){
  case 0:
    //body
    break;
  case 2:
    //body
  case 3:
    //body FALL THROUGH CASE
    break;
  case 4: //multiple case label
  case 5:
    //body
    break;
  default: //default & missing case
    break;
}
```
</td>
<td>

```c
goto *JTab[x]; //goto jump table
```
</td>
<td>

```py
switch:
  movq %rdx, %rcx
  cmpq $6, %rdi $ x:6 (effectively x-6)
  ja .L8 # 6 is the default minimum case
  jmp *.L4(,%rdi, 8) # address = rdi*8 + .L4

.section  .rodata
  .align 8 # target requires 8 bytes
.L4: # start of table
  .quad .L8 # x = 0
  .quad .L3 # x = 1
  .quad .L5 # x = 2
  .quad .L9 # x = 3
  ...
```
</td>
</tr></td></table>

jtab - array of addresses. Addresses are to code blocks
must scale by a factor of 8, hence rdi*8
.L4 start of table
address in this case is calculated as .L4 + x*8 for [0, 6]
same cases map to the same label (eg. default and unincluded case)


## Examples of Assembly
```py
.L3: # label
  movq %rsi, %rax # moves rsi to rax (return register)
  imulq %rdi, %rax # multiplies rax by rdi, stores into rax
  ret # returns rax always
```

## Register Associations
%rip - instruction pointer
%rax - return value

**Default Argument Registers**
1. %rdi
2. %rsi
3. %rdx
4. %rcx
5. %r8
6. %r9

![](@attachment/Clipboard_2022-04-14-18-17-08.png)
![](@attachment/Clipboard_2022-04-14-18-17-54.png)

[^1]:jmp - unconditional jump
je - equal
jne - not equal
jg - greater
jge - greater or equal
ja - above (unsigned)
jae - above or equal (unsigned)
jl - lesser
jle - less or equal
jb - below (unsigned)
jbe - below or equal (unsigned)
jo - overflow
jno - not overflow
jz - jump if zero
jnz - not zero

[^2]: https://cs.brown.edu/courses/cs033/docs/guides/x64_cheatsheet.pdf

















