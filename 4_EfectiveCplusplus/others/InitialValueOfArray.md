# What is the initial Value of int array?

## Problem
When declaring an array like this:
~~~c++
int array[10];
~~~
or 
~~~c++
int* p = new int[5]; 
~~~
What is the initial value of the integers??

## Summary
~~~c++
int a[10];  
// Global variable in Data Segment -> initialised to 0

void foo(void) {
    int b[10]; 
    // Automatic variable in Stack-->garbage value

    static int c[10]; 
    // Static variable in Data Segment --> initialised to 0

    int* p = new int[5]; 
    // Dynamic variables in Heap-->garbage value    
    
    // Initialized by compilier
    int* p = new int[5]();// initialised to 0
    int* p = new int[5]{};// initialised to 0 (Modern C++)
    int* p = new int[5]{ 1,2,3 }; 
    // 1  2  3  0  0  (Modern C++)
}
~~~
- Depends on **storage class**.
    - Global or Static (in data segment)
        - Initialized to zero.
    - Others (stack or heap)
        - garbage value
- However, it is a good practice to 
    1. Using **vector** instead of **new int[n]**, due to the [RAII principle](../EC_3_ResourceManagement/RAII.md).        
    2. always manually initialise function variable.
    ~~~c++
    int b[10] = {0};
    ~~~

## Detailed Information
### Why are function locals (auto storage class) not initialized when everything else is?
- C is close to the hardware; that's its greatest strength and its biggest danger.
- The reason **auto** storage class objects have random initial values is because they are allocated on the **stack**, and a design decision was made **not to automatically clear these** (partly because they would need to be cleared on every function call).

- Likewise, **dynamic** variables, allocated in **Heap**, are initialized with garbage values.

- On the other hand, the variables in **Data segment** only have to be cleared once. Plus, the OS has to clear allocated pages for security reasons anyway. So the design decision here was to specify zero initialization. 

- Why isn't security an issue with the stack, too? Actually it is cleared, at first. The junk you see is from *earlier instances of your own program's call frames* and the library code they called.

## Prerequisite
- [Storage class](../others/StorageClasses.md)
- [Memory Layout](../others/MemoryLayout.md)

## Ref
1. [initial value of int array in C](https://stackoverflow.com/questions/1414215/initial-value-of-int-array-in-c)
2. [How can I make new default-initialize the array of primitive types?](https://stackoverflow.com/questions/2468203/how-can-i-make-new-default-initialize-the-array-of-primitive-types)

### Date
2022/05/21