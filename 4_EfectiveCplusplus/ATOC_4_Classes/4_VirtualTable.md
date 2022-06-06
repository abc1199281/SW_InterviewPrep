# What is the Virtual Table (v-table)?
###  Reference: 4.4: virtual function
## Summary
0. Motivation:
    - Implementation detail for **virtual functions**.
    - C++ uses a special form of late binding known as the virtual table.
    - The virtual table is a lookup table of functions used to resolve function calls in a dynamic/late binding manner.
    
1. a.k.a, 
    - virtual function table
    - vtable
    - dispatch table


## Detailed information
1. First, every class that uses virtual functions (or is derived from a class that uses virtual functions) is given its own virtual table. This table is simply a static array that the compiler sets up at compile time. A virtual table contains one entry for each virtual function that can be called by objects of the class. Each entry in this table is simply a function pointer that points to the most-derived function accessible by that class.

2. The compiler also adds a hidden pointer that is a member of the base class, which we will call *__vptr. *__vptr is set (automatically) when a class instance is created so that it points to the virtual table for that class. Unlike the *this pointer, which is actually a function parameter used by the compiler to resolve self-references, *__vptr is a real pointer. Consequently, it makes each class instance allocated bigger by the size of one pointer. It also means that *__vptr is inherited by derived classes, which is important.

3. Sample
~~~c++
class Base
{
public:
    // This is the vtable, responsible for Base class.
    VirtualTable* __vptr; 
    virtual void function1() {};
    virtual void function2() {};
};

class D1: public Base
{
public:
    // This is inhereted, responsible for D1 class.
    // VirtualTable* __vptr; 

    // This is override, so the table call this pointer
    // D1::function1()
    virtual void function1() {}; 

    // This is not overrided, so the table call the function pointer 
    // in the base, i.e., Base::function2();
    // virtual void function2(){}; 
};

int main()
{
    D1 d1;

    // 1. dPtr is a base pointer, it only points to the Base portion of d1
    // 2. *__vptr is also in the Base portion of the class, so dPtr has access to this pointer.
    // 3. Note: dPtr->__vptr points to the D1 virtual table! 
    Base* dPtr = &d1;

    // 1. the program recognizes that function1() is a virtual function.
    // 2. uses dPtr->__vptr to get to D1’s virtual table.
    // 3. It looks up which version of function1() to call in D1’s virtual table, D1::function1().
    // 4. dPtr->function1() resolves to D1::function1()!
    dPtr->function1();

    return 0;
}
~~~

4. Calling a virtual function is slower (<25%) than calling a non-virtual function for a couple of reasons
    - we have to use the *__vptr to get to the appropriate virtual table.
    - we have to index the virtual table to find the correct function to call.
    - Also as a reminder, any class that uses virtual functions has a *__vptr, and thus each object of that class will be bigger by one pointer. Virtual functions are powerful, but they do have a performance cost.


## Ref:
[1] [Learn C++, The virtual table](https://www.learncpp.com/cpp-tutorial/the-virtual-table/)

### Date
2022/06/07