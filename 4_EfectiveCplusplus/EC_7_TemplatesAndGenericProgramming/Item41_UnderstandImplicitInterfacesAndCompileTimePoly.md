# Item 41: Understand implicit interfaces and compile-time polymorphism

### Reference: Item 41


## Introduction
1. Development of template
    - "Type safe" containers are the initial motivation of template.
        - Now, containers are just a small part of C++ template.
    - "Generic programming" enables the independiency between src code and type of objects.
    - Template is Turing-complete-->Template metaprogramming
    - The programs that execute inside C++ compilers and that stop running when compilation is complete.

## Summary

1. Comparison of Metaprogramming with OOP.

||Object-oriented| Metaprogramming|
|-|-|-|
|Interfaces, |Explicit | Implicit|
| based on ...| function signatures| valid expressions |
|Polymorphism, |Run-time|Compile-time|
| based on ...| dynamic binding|overloaded functions|
|check when...|compile-time|compile-time|

2. Things to Remember
    1. Both classes and templates support interfaces and polymorphism.
    
## Detailed Information
1. function signatures v.s. valid expressions
~~~c++
// function signatures (ctor, dtor, copy, size, etc)
class Widget{
public:
    Widget();
    virtual ~Widget();
    virtual std::size_t size() const;
    virtual void normalize();
    void swap(Widget& other);
};

// valid expressions
// w.size(), operator!=
template<typename T>
void doProcessing(T& w){
    if (w.size()) > 10 && w!=someNastyWidget){
        //...
    }
}
~~~

### Date
2022/12/25