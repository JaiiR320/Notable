---
attachments: [Clipboard_2023-03-23-14-01-25.png]
tags: [CS4401]
title: Stack 3
created: '2023-03-23T17:04:40.776Z'
modified: '2023-03-23T18:47:42.171Z'
---

# Stack 3
look for syclic patterns
figure out GEF
stack frame - frame created by program that stores stuff
rbp - bottom frame pointer
adjust where stack pointer is by skipping push instruction
push instruction adds 8 bytes to stack, so skipping does not mess with alignment
gdb places breakpoint after prologue, skips setup of frame pointer
putting * or not may skip the prologue

3 instructions in prologue
sets up stack frame
- push rbp pushes base pointer of previous stack frame, so we can update later
- copies rsp into rbp
- allocates space on stack by subtracting 0x50 from rsp

# sig seg v vs sig bus
- segfault virtual address is legal, but doing something illegal to memory
- sparse address space
- use address that is not a legal address is sig bus error
- sig ill, illegal instructions

# stack 4
code injection
checksec - check for NX flag disabled, also RWX
vmmap - shows memory space and its permissions

when a process starts
stdin stdout stderr all open
  0      1      2   file descriptor

fd = open(...)
sendFile(1, fd, 0, 0xff)
source = fd, target = 1 = stdout, offset = 0, number of bytes = 0xff

![](@attachment/Clipboard_2023-03-23-14-01-25.png)
this asm pushes the string "./file.txt" onto the stack somewhere which is located at rsp now because of the push calls

perfroming on edx esi etc. clears the top 32 bits
mov rdx, 0 will include a null byte, which we don't necessarily want

rax is the output register

https://syscalls64.paolostivanin.com/
shows 

no op instruction executes but does nothing
nop sled take 4000 nops, add them to shell code
increases size of shell code artificially
shell code should print flag already
we can land anywhere inside the nop sled and execute theose nops then execute script form beginning
make stack bigger by adding more environment variables


# questions
how to get docker working

