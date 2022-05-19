# What is the difference between argument & parameter?

## Answer
~~~c++
void SomeFunc(Widget w);
// w is parameter, pass by reference.

Widget wid;
SomeFunc(wid);
// wid is argument, w is parameter.
// keep its status of 'rvalue' or 'lvalue'

someFunc(std::move(wid))
// std::move(wid) is argument, w is parameter.
~~~
- Why this?
    - **perfect forwarding**.
- **parameter** is 
    - function's variable (to be initialized.)
    - lvalue.
- **argument** is
    - the statement that call the function and pass variable.
    - can be rvalue or lvalue.

## Ref:
[1] Effective Morden C++, p3-p4.