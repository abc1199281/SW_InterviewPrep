# What is the template with value argument or non-type parameter?

### Reference: 6.2.2 value template argument

## Summary
1. Motivation:
    - template with size / address. 
2. Definition:
    - A template parameter where the type of the parameter is predefined and is substituted for a constexpr value passed in as an argument.
    - Content:
        - constant expressions, 
        - addresses of functions or objects with external linkage
3. Sample:
    ~~~c++
    //non-type template
    template<typename T, int N> 
    class Buffer{
        using value_type = T;
        constexpr int size(){return N;}
        T[N];
    }

    // Donot utilize memory store (dynamic)
    Buffer<char, 1924> glob; // static

    int fct(){
        // stack, autonomic variable
        Buffer<int, 10> buf;
        // N must be a constant expression. 
    }    
    ~~~

## Detailed Information
1. One of the parameterized types in template.
    - Constrained Template Arguments
    - **Value Template Arguments**
    - Template Argument Deduction

### Date
2022/06/07
