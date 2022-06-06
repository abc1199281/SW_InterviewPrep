# What is the static assertions?

###  Reference: 3.5.3: Static assertions

## Summary
1. Motivation:    
    - If an error can be found at compile time, it is usually preferable to do so.
2. Syntax
    - Can be used for anything that can be expressed as constant expression.
    ~~~c++
    static_assert(4<=sizeof(int),"integers are too small!");

    constexpr double C = 123;
    void f(double speed){
        // calculated at compile time.
        constexpr double local_max = 160.0/(60*60); 

        // Error, speed is not const. expression
        static_assert(speed<C,"can't go that fast.");

        // OK
        static_assert(local_max<C,"can't go that fast.");
    }
    ~~~
3. Application:
    - The most important uses of static_asser t come when we make assertions about types used as parameters in **generic programming**.

### Date
2022/06/06