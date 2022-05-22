# Can I initialize an array with variable specified by **const**?

## Questions
- q1: We cannot initialize an array with non-const variable, why?
    ~~~c++
    int x = 12;
    char pz[x]; 
    ~~~
- q2: Can we initialize an array with variable specified by **const**? (case 1)
    ~~~c++
    const int x = 12;
    char pz[x]; 
    ~~~
- q3: Can we initialize an array with variable specified by **const**? (case 2)
    ~~~c++
    int a = 12;
    const int x = a;
    char pz[x]; 
    ~~~

## Summary
- Conclusion:
    - *If dynamic size of array is required, use **std::vector***
- a1: 
    - Nope;
    - It is **not** standard C++.
    - Although it standard in C99.

- a2: 
    - It's simply a limitation of the language. 
    - The sizes of arrays need to be **constant expressions**
    - In **C**,
        - Only something like a **literal constant** (#Define x 3) or a **sizeof expression** or such like, but **not a const-typed variable**.
    - In **C++**, more constant expressions are included, such as 
        - *static const int*, 
        - *const int*
        - *constexpr* 
- a3:
    - *const int x=a* is not a constant expression.
    - a is mutable, so x is considered as non-const.
    - Counter-examples
    ~~~c++
    // case 1: Flow analysis is required, too complex.
    int a = foo();
    const int x=a;
    // case 2
    int a = 12;
    const int x=a;
    ~~~


## Ref
1. [Dynamic Array in Stack?](https://stackoverflow.com/questions/1204521/dynamic-array-in-stack)
2. [Can A const variable used to declare the size of an array in C?](https://stackoverflow.com/questions/18848537/can-a-const-variable-be-used-to-declare-the-size-of-an-array-in-c)

### Date
2022/05/22