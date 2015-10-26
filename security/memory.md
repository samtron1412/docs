[TOC]

# Process Virtual Memory (VM)
Each process in a multi-tasking OS runs in its own *memory sandbox*. This sandbox is the virtual address space, which in 32-bit mode is always a 4GB block of memory addresses. These virtual addresses are mapped to physical memory by *page tables*, which are maintained by the operating system kernel and consulted by the processor (CPU with MMU - memory management unit).

The VM we're concerned with consists of the following principles:

1. Each process is given physical memory called the process's virtual memory space.
2. A process is unaware of the details of its physical memory (i.e. where it physically resides). All the process knows is how big the chunk is and that its chunk begins at address 0.
3. Each process is unaware of any other chunks of VM belonging to other processes.
4. Even if the process did know about other chunks of VM, it's physically prevented from accessing that memory.

<figure>
  <figcaption style="text-align:center;">Figure. Process Virtual Memory</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/virtualMemory.png" alt="virtual memory" title="virtual memory">
</figure>

# Memory Layout
## Process memory split
>Process memory split default on Linux and Windows

<figure>
  <figcaption style="text-align:center;">Process Memory Split</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/kernelUserMemorySplit.png" alt="kernel process memory split" title="kernel process memory split">
</figure>

## Standard user-mode process memory layout on Linux

<figure>
  <figcaption style="text-align:center;">Memory Layout</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/linuxFlexibleAddressSpaceLayout.png" alt="memory layout" title="memory layout">
</figure>

## Text segments, Data, BSS
### Definitions

>*Text segment*

A text segment , also known as a code segment or simply as text, is one of the sections of a program in an object file or in memory, which contains *executable instructions*.

As a memory region, a text segment may be *placed below the heap or stack* in order to prevent heaps and stack overflows from overwriting it.

Usually, the text segment is *sharable* so that only a single copy needs to be in memory for frequently executed programs, such as text editors, the C compiler, the shells, and so on. Also, the text segment is often *read-only*, to prevent a program from accidentally modifying its instructions.

>*Initialized Data Segment*

Contains the global variables and static variables that are initialized by the programmer.

Note that, data segment is *not read-only*, since the values of the variables can be altered at run time.

This segment can be further classified into initialized read-only area and initialized read-write area.

For instance the global string defined by `char s[] = “hello world”` in C and a C statement like `int debug=1` outside the main (i.e. global) would be stored in initialized read-write area. And a global C statement like `const char* string = “hello world”` makes the string literal “hello world” to be stored in initialized read-only area and the character pointer variable string in initialized read-write area.

*Ex*: `static int i = 10` will be stored in data segment and `global int i = 10` will also be stored in data segment

>*BSS* block started by symbol

Uninitialized data starts at the end of the data segment and contains all global variables and static variables that are initialized to zero or do not have explicit initialization in source code.

For instance a variable declared `static int i;` would be contained in the BSS segment.
For instance a global variable declared `int j;` would be contained in the BSS segment.

<figure>
  <figcaption style="text-align:center;">Text Segment</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/mappingBinaryImage.png" alt="text segment" title="text segment">
</figure>

>*Heap*

Heap is the segment where *dynamic memory allocation* usually takes place.

The heap area begins at the end of the BSS segment and grows to larger addresses from there.The Heap area is managed by `malloc, realloc, and free`, which may use the `brk and sbrk system calls` to adjust its size (note that the use of brk/sbrk and a single “heap area” is not required to fulfill the contract of malloc/realloc/free; they may also be implemented using mmap to reserve potentially non-contiguous regions of virtual memory into the process’ virtual address space). The Heap area is shared by all shared libraries and dynamically loaded modules in a process.

### Example
The size(1) command reports the sizes (in bytes) of the text, data, and bss segments. ( for more details please refer man page of size(1) )

1. Check the following simple C program

        #include <stdio.h>
        int main(void)
        {
          return 0;
        }

    Check by `size` command.

        [narendra@CentOS]$ gcc memory-layout.c -o memory-layout
        [narendra@CentOS]$ size memory-layout
        text       data        bss        dec        hex    filename
        960        248          8       1216        4c0    memory-layout


2. Let us add one global variable in program, now check the size of bss (highlighted in red color).

        #include <stdio.h>
        int global; /* Uninitialized variable stored in bss*/
        int main(void)
        {
            return 0;
        }

    Check by `size` command.

        [narendra@CentOS]$ gcc memory-layout.c -o memory-layout
        [narendra@CentOS]$ size memory-layout
        text       data        bss        dec        hex    filename
         960        248         12       1220        4c4    memory-layout

3. Let us add one static variable which is also stored in bss.

        #include <stdio.h>
        int global; /* Uninitialized variable stored in bss*/
        int main(void)
        {
            static int i; /* Uninitialized static variable stored in bss */
            return 0;
        }

    Check by `size` command.

        [narendra@CentOS]$ gcc memory-layout.c -o memory-layout
        [narendra@CentOS]$ size memory-layout
        text       data        bss        dec        hex    filename
         960        248         16       1224        4c8    memory-layout

4. Let us initialize the static variable which will then be stored in Data Segment (DS)

        #include <stdio.h>

        int global; /* Uninitialized variable stored in bss*/

        int main(void)
        {
            static int i = 100; /* Initialized static variable stored in DS*/
            return 0;
        }

    Check by `size` command.

        [narendra@CentOS]$ gcc memory-layout.c -o memory-layout
        [narendra@CentOS]$ size memory-layout
        text       data        bss        dec        hex    filename
        960         252         12       1224        4c8    memory-layout

5. Let us initialize the global variable which will then be stored in Data Segment (DS)

        #include <stdio.h>

        int global = 10; /* initialized global variable stored in DS*/

        int main(void)
          {
            static int i = 100; /* Initialized static variable stored in DS*/
            return 0;
          }

    Check by `size` command.

        [narendra@CentOS]$ gcc memory-layout.c -o memory-layout
        [narendra@CentOS]$ size memory-layout
        text       data        bss        dec        hex    filename
        960         256          8       1224        4c8    memory-layout

## Stack

>*Stack* is contained all local variables of functions. The stack might be decreasing or increasing when function call and end. Consist of many *stack frame*, each stack frame is corresponding with a function call.

<figure>
  <figcaption style="text-align:center;">Stack Function Call Layout</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/call_stack_layout.png" alt="Stack Function Call Layout" title="Stack Function Call Layout">
</figure>

*Stack Pointer* (%ESP): top of stack, lower address

*Frame Pointer* (%EBP): bottom of stack frame, higher address

*Return Address*  (%EIP)

### Function Call
Three phase

1. `Call` push parameters to stack, save %eip - instruction pointer (return address).

        push $arg1
        push $arg2
        push ...
        push $argn
        call <function>

2. `Prolog` save state of stack (save %ebp - frame pointer), allocate local memory for new function (plus %esp).

        push %ebp
        mov %esp, %ebp
        sub $0c, %esp

3. `Epilog` restore state of stack before call function.

        leave (leave = mov %ebp, %esp ; pop %ebp)
        ret (restore %eip, clean args)

### Recursion
Epilogues and prologues can make recursion performance worse

- use [tail call](http://en.wikipedia.org/wiki/Tail_call)
- or explicit [iteration](http://en.wikipedia.org/wiki/Iteration) instead

### Example function call

Let's see a simple C program:
<figure>
  <figcaption style="text-align:center;">Add Program</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/addProgram.png" alt="Add Program" title="Add program">
</figure>

main Prolog:
<figure>
  <figcaption style="text-align:center;">main function</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/mainProlog.png" alt="main function" title="main function">
</figure>

call add function:
<figure>
  <figcaption style="text-align:center;">call add function</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/callAdd.png" alt="call add function" title="call add function">
</figure>

add Prolog:
<figure>
  <figcaption style="text-align:center;">add Prolog</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/addProlog.png" alt="add Prolog" title="add Prolog">
</figure>

do add:
<figure>
  <figcaption style="text-align:center;">do add</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/doAdd.png" alt="do add function" title="do add function">
</figure>

full sequence:
<figure>
  <figcaption style="text-align:center;">call function sequence</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/fullSequence.png" alt="full call function" title="full call function">
</figure>

return from add
<figure>
  <figcaption style="text-align:center;">return from add</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/returnFromAdd.png" alt="return from add" title="return from add">
</figure>

return from main
<figure>
  <figcaption style="text-align:center;">return from main</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/returnFromMain.png" alt="return from main" title="return from main">
</figure>

full return sequence
<figure>
  <figcaption style="text-align:center;">full return sequence</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/fullReturnSequence.png" alt="full return sequence" title="full return sequence">
</figure>

# Example Demonstrate memory layout

A good example to demonstrate the *memory layout* and its stack info of the **user-mode process**, this example is for Linux.

C source file is quite simple:

```c
void func(int x, int y) {
    int a;
    int b[3];
    /* no other auto variable */
}

void main() {
    //sth
    func(72,73);
    //sth
}
```

The memory layout of a typical C's process is as below

<figure>
  <figcaption style="text-align:center;">Memory Layout</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="Figures/memory_layouts_linux.png" alt="Memory layout" title="Memory layout">
</figure>
