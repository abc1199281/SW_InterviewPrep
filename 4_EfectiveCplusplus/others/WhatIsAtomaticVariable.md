# What is automatic variable
## Simple answer
- local variable
- a.k.a, stack variable.
- When a variable is declared in a function, it becomes an automatic variable.
- Properties
    - lifetime of an automatic variable equals the block where it declared.
- It's simple. Why I need to know this?
    - Answer the following question.

## Detailed Answer
- Why Code 1 is **undefined behavior**,but Code 2 is safe?
- Code 1: undefined behavior
~~~c++
class MyVec(){

};
~~~
- Code 2: safe
~~~c++
vector<int>& return_automatic_vector(){    
    vector<int> a; 

    return a;
}
~~~

## Detailed information
- There are four storage classes, please see
    - [What is ]

## Ref
1. [Storage classes](https://home.csulb.edu/~pnguyen/cecs282/lecnotes/lec03.html)