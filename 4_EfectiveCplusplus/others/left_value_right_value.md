# What is left value, right value

## Summary
0. Motivation:
    - For **move semantic**.
1. left value:
    - after assignment (=), still exist.
    - Requirement: we can obtain the **address**.
    - all parameters are **lvalue**. 
    - cannot use **move operation**.
    ~~~c++
    class Widget{
    public:
        Widget(Widget&& rhs){ // move constructor.
            // we can get the address of "rhs"
            // -->"rhs" is lvalue whose type is rvalue reference.
        }
    }
    ~~~
2. right value:
    - after assignment (=), doesn't exist.
    - can use **move operation**.

## Detailed Information
### Can function be a lvalue? Yes
~~~c++
vector<int> vec={1,2,3};
vec[1]=99;// overload operator[]<-- function as lvalue
~~~

### More powerfull: prvalue (pure rvalue) & xvalue (expiring value)
- prvalue (e.g.,)
    - constant: 10, true
    - temporary result: 1+2
    - lambda expression
- xvalue:
    - A new concept to introduce **rvalue reference**.
    ~~~c++
    std::vector<int> foo(){
        std::vector<int> temp = {1,2,3,4};
        return temp;
    }
    std::vector<int> v = foo(); // a copy of temp-->redundant.
    /*
    c++11: compilier optimization (implicit rvalue conversion)
    static_cast<std::vector<int>&&>(temp)
    // move operation.
    */
    ~~~
### rvalue reference, lvalue reference
- Before c++11:
    - lvalue reference (T&)
    ~~~c++
    int a = 3;
    int&ar = a; // correct reference
    int&arr = 3; // incorrect
    ~~~
- After c++11:
    - rvalue reference (T&&)
    ~~~c++
    int&&a = 3; // correct
    int&&b = MyInt();// correct.
    ~~~
- std::move --> Forcely change lvalue into rvalue.
    ~~~c++
    int main(){
        static_cast<int&&>(7);// The expression belongs
        // to the xvalue category, because it is a cast 
        // to an rvalue reference to object type.

        std::move(7); // std::move(7) is equivalent to static_cast<int&&>(7).

        // 
    }
    ~~~

## Ref:
[1] Effective Morden C++, p3-p4.

### Date
2022/05/19