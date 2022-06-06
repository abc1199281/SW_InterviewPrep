# What is the Exception in C++?
###  Reference: 3.5.1: Exception
## Summary
0. Motivation:
    - Vector
        - Author of library: don't know when out of range.
        - users: don't know that is out of range.
1. Solution:
    - try/catch, 
    - If exception is throwed, program will do **stack-unwinding**, which return from function call stack back to caller.
    ~~~c++
    #include <stdexcept>
    try{
        v[v.size()]=7;
    }catch(out_of_range & error){
        ceer<<err.what()<<'\n';
    }
    ~~~

## Detailed information
1. Note:
    - During stack-unwinding, automatic variables' destructor will be called automatically.
    - Along with RAII, resource are much more safe.
2. **noexcept**: 
    - The function which should never throw exception
    - If exception is throwed, C++ call **std::terminate()**
    ~~~c++
    void user(int sz) noexcept
    {
        Vector v(sz);//...
    }
    ~~~

### Date
2022/05/22