# What is Stack Unwinding?

### Prerequisite
- [Memory Layout](/4_EfectiveCplusplus/others/MemoryLayout.md)
- [Storage Classes](/4_EfectiveCplusplus/others/StorageClasses.md)
- [RAII](/4_EfectiveCplusplus/ATOC_5_EssentialOperstions/RAII.md)

## Summary
0. Motivation:
    - Ususally talked about in connection with **except handling**.
1. Description
    - For *automatic (Stack)* variable:
        - *stack-unwind* can provide **exception-safe**.
        - Because destructor is automatically called after existing scope.
    - For *Dynamic (Heap)* variable:
        - From definition, there is no *stack-unwind*.
        - With **RAII**, **Holding a resource** is tied to **object lifetime**, and thus **stack-unwind** is also hold for *dynamic variable*.
        - Then, *Dynamic (Heap)* is also *expetion-safe* with *RAII*.
        


## Detailed information
1. Example
~~~c++
void func(int x)
{
    char* pleak = new char[1024]; 
    // dynamic variable in heap, 
    // might be lost->memory leakage

    string::s{"hello world"};
    // automatic variable in stack,
    // will be properly destructed.

    if (x) throw std::runtime_error("boom")

    delete [] pleak; 
    // will only get here if x==0.
    // If x!=0, throw exception.
}
int main()
{
    try{
        fun(10);
    }catch(const std::exception& e){
        return 1;
    }
    return 0;
}
~~~
- Memory leakage of *pleak* if an exception is thrown. However, memory allocated to *s* will be properlly released by destructor in any case.
- The object allocated on the stack are **unwound** when the scope is exited.
- This operation (a.k.a., *Stack unwinding*) is done by the compiler inserting calls to destructors of automatic (stack) variables.
- How about **dynamic variable**?
    - Now, a very powerful concept is **RAII**.
    - RAII here helps us to provide  **exception safety guarantees**.
    - RAII also helps us manage resources like memory, database connections, etc.

## Ref:
[1] [What is stack unwinding](https://stackoverflow.com/questions/2331316/what-is-stack-unwinding)

### Date
2022/05/21