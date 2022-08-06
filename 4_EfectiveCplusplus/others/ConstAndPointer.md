# **const** with Pointers?

## Summary
- If const is on the left of *, data is const.
- If const is on the right of *, pointer is const.

~~~c++
// 1.
const int i = 9;
i=6;  // Compile Error

// 2. 
const int *p1 = &i; // data is const, pointer is not
*p1 = 5; // Compile Error
p1++; // OK

// 3.
int * const p2=p1; // pointer is const, data is not
*p1 = 5;//OK
p2++; // Error

// 4. 
const int* const p3; // both are const

// 5. 
int const *p4 = &i; // data is const, pointer is not.
const int *p5 = &i;
~~~


## Details
- Cast away data
    - Cast is not a good thing, you should avoid it.
~~~c++
const int i = 9;
// i=6; // not work
const_cast<int&>(i) = 6;

int j;
static_cast<const int&>(j) = 7; // fail.
~~~
## Why use const
1. Guards against inadvertent write to the variable.
2. Self documenting
3. Enables compiler to do more optimization, making code tighter.
4. const means the variable can be pu in ROM.

## Ref
1. [Advanced C++: const](https://youtu.be/7arYbAhu0aw?list=PLE28375D4AC946CC3)

### Date
2022/08/06