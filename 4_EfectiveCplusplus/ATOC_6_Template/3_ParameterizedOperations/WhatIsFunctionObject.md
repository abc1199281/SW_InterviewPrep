# What is the Function Object?

### Reference: 6. 3 Parameterized operation

## Summary
0. Definition:
    - an object that can carry data and be called like a function
    - a.k.a., **functor**
1. Sample :
    - simplified version of *std::accumulate()*.
    ~~~c++
    template<template T>
    class Less_than{
        const T val;
    public:
        Less_than(const T&v): val{v}{}
        bool operator()(const T&x) const{
            return x<val;
        }
    }
    Less_than lti{42}; // compare with 42    

    void fct(int n, const string&s){
        bool b1 = lti(n);        
    }
    ~~~

## Detailed Information
1. Argument of algorithm
    ~~~c++
    template<typename C, typename P>
    int count(const C&c, P pred)
    {
        // pred: predicate, return fale/true.
        int cnt = 0;
        for(const auto & x: c)
            if(pred(x))
                ++cnt;
        return cnt;
    }
    void f(const Vector<int>& vec, const list<string>& lst, int x, const string& s){
        cout<<"number of values less than"<< x<<":"<<count(vec, Less_than{x})<<endl;
    }
    ~~~
    - can be inline, high performance.
    - can also bring data with initialization.
    - a.k.a., **policy object**
2. Parameterized Operations
    - Function template
    - **Function object** 
        - an object that can carry data and be called like a function
    - Labda expression
        - a shorthand notation for a function object.

### Date
2022/06/11