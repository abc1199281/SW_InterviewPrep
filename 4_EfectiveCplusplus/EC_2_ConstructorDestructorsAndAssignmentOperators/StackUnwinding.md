# What is the RAII (Resource Acquisition is initialization)?

## Simple answer
0. Motivation:
    - Programming idiom used in OOP language.
    - As long as RAII is hold, **if there are no object leaks, there are no resource leaks**.
    - Method: 
        - **Holding a resource** is tied to **object lifetime**.
        - **exception-safe** && concise.
    - Notes: 
        - Not coincide with **Scope**.
        - *Variables allocated on **free store** have lifetimes unrelated to any given scope*. 
1. Rules of three
    - There are three member functions that go together.
        1. destructor.
        2. copy constructor.
        3. assignment operator.
    - If you need to define either of them, you must define all of them. Or, you should not define any of them.
2. **Note:** In C++11, there should be rules of five (a.k.a. **rule of big 5**)
    1. destructor.
    2. copy constructor.
    3. copy assignment operator.
    4. move constructor.
    5. move assignment operator.

## Detailed Information
### Limitation
- RAII only works for resources acquired and released (directly or indirectly) by stack-allocated objects, where there is a well-defined static object lifetime.

## Ref:
[1] [Wiki: RAII](https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization)

### Date
2022/05/21