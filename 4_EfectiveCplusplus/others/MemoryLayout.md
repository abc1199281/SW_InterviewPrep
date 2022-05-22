# What is the Memory Layout in C/C++?
## Summary
- The memory of a C++ program running on Unix consists of the following sections:

    1. Text segment
    2. Static data region
        1. Initialized data segment            
        2. Uninitialized data segment
        - **Global (extern), or static** variables.
    3. Stack
        - **Automatic** variables.
    4. Free Store (or Heap)
        - **Dynamic** variables.
        - If not freed properlly, there is **memory leak**.

![Memory Layout](https://media.geeksforgeeks.org/wp-content/uploads/memoryLayoutC.jpg)

## Detailed Information
1. Text segment
    - a.k.a., **code segment**,**Text**
    - As a memory region, a text segment may be placed below the heap or stack in order to prevent heaps and stack overflows from overwriting it.
    - the text segment is often read-only, to prevent a program from accidentally modifying its instructions.
2. Static data region
    1. Initialize Data segment
        - a.k.a, **Data segment**
        - Storage class: 
            - Initialized *global variables and static variables*.
        - not read-only
    2. Uninitialize Data segment
        - a.k.a., **bss**, **block started by symbol**
        - Data in this segment is initialized by the kernel to arithmetic 0 before program starts executing.
        - Storage class: 
            - *global variables and static variables* without explicit initialization or initialized to 0.
    3. Reason: 
        - Lifetime of *global and static variables* are **Till the end of program**.
        - So, the size of these memory are constant during program.
3. Stack
    - Each time a function is entered, a **stack-frame** is allocated and is used to hold the values of all automatic variables declared in the function.
    - Stack frame also hold the addressing information, telling the CPU how to "get back" to the calling function.
    - When function is exited, the stack-frame is deallocated.
    - Adjoined the heap area and grew in the opposite direction.
    - When stack & heap pointer meet, free memory was exhausted. 
    - With Modern large address space and virtual memory techniques, they can be placed almost anywhere, but they still typically grow in opposite directions.

4. Heap (or Free Storage)
    - Usually, Free storage equals to Heap. - Begins at the end of BSS.
    - managed by malloc/free/new/delete.
    - **If you try to use the pointers to freed memory after you free them, it will cause undefined behavior.**
        - Solution:
            - set the freed pointers to **nullptr** immediately after *delete*.
    - Implementation
        - mmap to reserve potentially non-contiguous regions of virtual memory into the process' virtual address space.
## Example
~~~c++
#include <stdio.h>
 
int g1; /* Uninitialized variable stored in bss*/
int g2=100; /* Initialized variable stored in DS*/
 
int main(void)
{
    static int i; /* Uninitialized static variable stored in bss */
    static int j=100; /* Initialized static variable stored in DS */
    return 0;
}
~~~

### Relationship to Class storage
- Block scope variables (**including function parameters**) are **automatic** storage (**stack**) by default, except **static** keyword.
- Dynamic variables **(Heap)** are allocated at run time using **new**/**malloc** and **delete**/**free**.

### Note: 
1. Good examples are illustrated in UIUC's resource [5](https://courses.engr.illinois.edu/cs225/sp2022/resources/stack-heap/).
2. It can be examed via **size** command as described in [4](https://www.geeksforgeeks.org/memory-layout-of-c-program/).

## Ref
1. [Memory Layout in C](https://www.geeksforgeeks.org/memory-layout-of-c-program/)
2. [Storage Classes](http://faculty.cs.niu.edu/~mcmahon/CS241/Notes/storage_class.html)
4. [Experiments](https://www.geeksforgeeks.org/memory-layout-of-c-program/)

### Date
2022/05/21