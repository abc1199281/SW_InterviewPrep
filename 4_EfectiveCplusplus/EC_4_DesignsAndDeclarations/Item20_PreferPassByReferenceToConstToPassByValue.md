# Item 20: Prefer pass-by-reference-to-const to pass-by-value

### Reference: Item 20

## Summary
- Prefer pass-by-reference-to-const over pass-by-value.
    - Reduce ctor/dtors
    - It's typically more efficient and it avoids teh slicing problem
- The rule doesn't apply *only* to 
    - build-in types 
    - STL iterators,
    - and function object types.
- *Small user-defined types are not necessarily good
pass-by-value candidates*

## Detailed Information
- Reduce ctor/dtors
    ~~~c++    
    bool validateStudent(Student s); // require ctor/dtor of Student

    bool validateStudent(const Student& s); // no ctor/dtor of Student
    ~~~
- Slice problem
    ~~~c++
    class Window{};
    class WindowScrollBars: public Window{};

    bool ProcessWindow1(Window w); // implicit conversion,
    bool ProcessWindow2(const Window w);


    WindowScrollBars wb;
    ProcessWindow1(wb); // base class, slicing problem
    ProcessWindow2(wb); // derived class
    ~~~
- Implementation detail:
    - Reference is implemented by pointers
    - For STL/Built-in types/ function object, pass by value is preferred.
    - *Small user-defined types are not necessarily good
pass-by-value candidates*

### Date
2023/01/04