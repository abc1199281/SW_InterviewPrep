# What is the difference between **const** and **constexpr**?
###  Reference: 3.5.1: Exception
## Summary
- **const**
    - Mean: I promised not to change this value.
    - Motivation: specify interfaces
    - Time: can be calculated at run-time.
- **constexpr**
    - Mean: To be evaluated at compile time.
    - Motivation: specify constants, to allow placement of data in read-only memory.
    - Time: **Must** be calculated at compile-time.


## Detailed information
- Basic usage
~~~c++
constexpr int dmv = 17; // named constant.
int var = 17; // not a constant
const double sqv = sqrt(var);// computed at run-time

// Error: sqrt is not a constant expression.
constexpr double sqv2 = sqrt(var); 
~~~
- **Constant Expression**
    - The function should be very simple.
    - The function **cannot** change local variable's value.
    - The function **can** use for loop or self's local variable..
~~~c++
constexpr double square(double x){return x*x;}
constexpr double max1 = 1.4*square(17);  // OK
constexpr double max2 = 1.4*square(var); // Error
const double max3 = 1.4*square(var); // OK.

constexpr double nth(double x, int n)
{
    double res = 1;
    int i = 0;
    while(i<n){
        res*=x;
        ++i;
    }
    return res;
}
~~~

### Date
2022/06/06