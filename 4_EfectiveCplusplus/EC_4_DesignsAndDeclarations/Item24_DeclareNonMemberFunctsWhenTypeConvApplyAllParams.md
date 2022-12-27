# Item 24: Declare non-member functions when type conversions should apply to all parameters.

### Reference: Item 24

## Summary
- If you need type conversions on all parameters to a function, the function must be a non-member.
- Motivation:
    ~~~c++
    class Rational{/*...*/};
    Rational onHalf(1,2);
    Rational onEight(1,8);
    Rational r1 = oneHalf * 2; // oneHalf.operator*(2), fine
    Rational r2 = 2 * oneHalf; // 2.operator*(oneHalf), error!
    ~~~

## Detailed Information
1. What compilers see:    
    ~~~c++
    const Rational temp(2);
    Rational r1 = oneHalf * temp; // fine with non-explicit operator*()
    class Rational{
    public:
        //non-explicit operator*()
        const Rational operator* (const Rational& rhs) const; 
    };
    ~~~
2. Solution: Non-member function
    - Allowing compilers to perform implicit type conversions on all arguments.
    - Note: this should not be a frind function to the class.
    ~~~c++
    const Rational operator*(const Rational& lhs, // now a non-member
                             const Rational& rhs) // function
    {
        return Rational(lhs.numerator()*rhs.numerator(),
                        lhs.denominator()*rhs.denominator());
    }                             
    ~~~

### Date
2022/12/27