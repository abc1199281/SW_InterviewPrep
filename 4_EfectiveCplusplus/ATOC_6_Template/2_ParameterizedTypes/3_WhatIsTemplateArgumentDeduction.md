# What is the Template Argument Deduction?

### Reference: 6.2.3 Template Argument Deduction

## Summary
1. Motivation:
    - Make type deduction (easier with risk.)

2. Sample:
    ~~~c++
    pair<int, double> p = {1,5.2};

    auto p = make_pair(1, 5.2); // stl method.
    
    pair p = {1, 5.2};// Since C++17
    ~~~

## Detailed Information
1. One of the parameterized types in template.
    - Constrained Template Arguments
    - Value Template Arguments
    - **Template Argument Deduction**
2. C-style string literal is *const char* *
    ~~~c++
    template<typename T>
    class Vector{//...        
    }

    Vector<string> s1{"hello","world"} //Vector<string>
    Vector s2{"hello","world"} // Vector<const char*>
    Vector s3{"hello"s,"world"s} // Vector<string>

    // Error: initializer list is not homogenous.
    Vector s4{"hello"s,"world"} 
    ~~~
3. *Deduction guide*
    - If we cannot deduce argument, *deduction guide*.
    - Effect of deduction guide is subtle, so it is best to design class templates so that deduction guides are not needed.
    ~~~c++
    template<typename T>
    class Vector2{
    public:
        using value_type = T;
        //...
        Vector2(initializer_list<T>);

        template<typename Iter> 
        Vector2(Iter b, Iter e)->Vector2<typename Iter::value_type>;
    }

    Vector2 v1{1,2,3,4,5}; // int.
    Vector2 v2(v1.begin(), v1.begin()+2);
    ~~~

### Date
2022/06/07