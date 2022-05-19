# [Item 42] What is the difference between .emplace_back() & .push_back()

### Related items:
- *Item 42: Consider emplacement instead of insertion.*

## Summary
1. **.emplace_back()**:
    - Declaration
    ~~~c++
    void emplace_back(Args&...)
    ~~~
    - The new element is **constructed in place** using **args** as the arguments for its constructor.
2. **.push_back()**
    - The content of val is **copied (or moved)** to the new element. This might make unnecessary copies.

## Detailed information
1. **.emplace_back()**:
    - Instead of taking a **value_type** it takes a **variadic list** of arguments, so that means that you can now **perfectly forward** the arguments and construct directly an object into a container without a temporary at all.

2. **.push_back()**
    - The content of val is **copied (or moved)** to the new element.
    - What happened:
        1. Constructor->temporary object
        2. Copy of the temporary object being constructed in the memory of container.
            - move constructor will be called if exist.
        3. Destructor will be called.

## Why not always **.emplace_back()**
- Constructor misleading
e.g., 
~~~c++
std::vector<std::vector<int>> vec1, vec2;
// vec1.push_back(1000000);  // compile error 
vec2.emplace_back(1000000);
std::cout << "Vector Size = " << vec2.at(0).size() << std::endl;
~~~
output
~~~c++
Vector Size = 1000000
~~~

## Ref:
[1] [What is the difference between new/delete and malloc/free?](https://stackoverflow.com/questions/4303513/push-back-vs-emplace-back)

[2] [emplace_back vs. push_back](https://yasenh.github.io/post/cpp-diary-1-emplace_back/)