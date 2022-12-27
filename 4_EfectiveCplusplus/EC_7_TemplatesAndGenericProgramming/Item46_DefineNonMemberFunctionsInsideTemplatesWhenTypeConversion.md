# Item 46: Define non-member function inside templates when type conversions are desired

### Reference: Item 46

## Summary
- When writing a class template that offers functions related to the template that support implicit type conversions on all parameters, define those functions as **friends inside the class template**.

- Template version of Item 24.
    ~~~c++
    template<typename T>
    class Rational{
    public:
        Rational(const T& numerator = 0, const T& denominator = 1);
        const T numerator() const;
        const T denominator() const;
    };

    template<typename T>
    const Rational<T> operator* (const Rational<T>& lhs,
                                 const Rational<T>& rhs)
    {/*...*/}

    // target:
    Rational<int> oneHalf(1,2);
    Rational<int> result = oneHalf*2; // error!
    ~~~

## Detailed Information
1. Problem formulation
    - In templates, compilers do not know which function we want to call.
        - Compilers try to figure out what function to instantiate from the template named operator*.
        - The problem is, they can't. Because the deduced types don't match.
    - **Implicit type conversion functions are never considered during template argument deduction.**
    - Order (cannot feed back loop.):
        1. Template: compiler generate code (known types)
        2. function exist
        3. implicit type conversion during function call.
        - We cannot expect generated code to do implicit type conversion.

2. Solution 1 (temp): frind functions
    - Because function exists before compile instantiate template,
    - Implicit type conversion is feasible.
    - Note: linkage error.
        - Declared in a class, no definition. 
    ~~~c++
    template<typename T>
    class Rational{
    public:
        // Note, inside template class,
        //  Rational = Rational<T>, a kind of shorthand.
        friend const Rational operator*(const Rational& lhs,
                                        const Rational& rhs)
    };
    template<typename T>
    const Rational<T> operator*(const Rational<T>& lhs,
                                const Rational<T>& rhs)
    {/*...*/}
    ~~~

3. Solution 2: frind functions
    - Solve linkage error.    
    ~~~c++
    template<typename T>
    class Rational{
    public:
        friend const Rational operator*(const Rational& lhs,
                                        const Rational& rhs){
            return Rational(lhs.num()*rhs.num(), lhs.den()*rhs.den());
        }
    };
    ~~~
    
### Date
2022/12/27