# What is the difference between argument & parameter?

## Summary
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
    - Only **lvalue**.
- **argument** is
    - the statement that call the function and pass variables.
    - Tips: 
        ~~~c++ 
        int main(int argc, char* argv){return 0;} // argument count, argument vector
        ~~~
    - can be rvalue or lvalue, which is important to **perfect forwarding**.

## Ref:
[1] Effective Morden C++, p3-p4.
### Date
2022/05/19