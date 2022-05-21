# Why can I return a local declared vector?

## Questions
- In a helper function,
- q1: we all know that returning a pointer to a local variable is dangerous, why?
- q2: Why return a *new* object is safe?
- q3: Why return a local declared vector/RAII object prefered?
- q4: Why return a reference to a local variable is dangerous?

## Summary
- a1: 
    - A pointer to *local (automatic) variable*, which is allocated on *stack*, will be invalid after the scope of function. This leads to *dangling* pointer, a pointer that points to invalid data.. 

- a2: 
    - A pointer to *dynamic variable*, which is allocated on *heap*, will be valid. Please note that programmer must delete properly to avoid memory leakage.

- a3: 
    - Because of **move-semantic** and **return value optimization** in C++11, as long as RAII is followed, the return (pass by value) is preferred. 

- a4:
    - C++ function can return a reference in a similar way as it returns a pointer.
    - When a function returns a reference, it returns an implicit pointer to its return value.
    - The same as a1, this is dangurous.

## Detailed Information
### Sample questions
~~~c++
class Cube;
Cube* CreateCube(){
    // local variable
    Cube c(20);
    return &c;
}
Cube* CreateCube2(){
    // locally newed variable-->local variable?
    Cube c = new Cube(20); 
    return c; 
}
vector<int>* CreateVec1(){
    // local declared vector, we don't new it!?
    vector<int>* rtn = new std::vector<int>(3,0); 
    return rtn;
}
vector<int> CreateVec2(){
    // local declared vector, we don't new it!?
    vector<int> rtn{1,2,3}; 
    return rtn;
}
Cube CreateCube3(){
    // local variable, why it works!?
    return Cube c(10);
}
Cube& CreateCube4(){
    // local variable
    Cube c(20);
    return c;
}
int main(){
    // Case 1: Undefined behavior
    Cube *c1 = CreateCube();
    double r1 = c1->getVolume(); 

    // Case 2: Works
    Cube *c2 = CreateCube2();
    double r2 = c2->getVolume();     
    delete c2;   // without delete->memory leakage.
    c2 = nullptr; // good practice to set nullptr

    // Case 3: OK, Like Case2
    // but, Case 4, return local variable is preferred.
    vector<int>* vec1 = CreateVec1();  
    delete vec1;
    vec1 = nullptr;  

    // Case 4: 
    // Return a local declared vector is prefered in C++11.
    vector<int> vec2 = CreateVec2();

    // Case 5: Works.
    Cube c3 = CreateCube3();
    double r3= c3.getVolume();

    // Case 6: Fails
    Cube c4 = CreateCube4();
    double r4= c4.getVolume();
}
~~~

### Detailed discussions
- Case 1:
    - Helper function: 
        - return a "pointer to a stack variable".    
    - After caller gets the pointer, the invalid stack memory can be overwritten at anytime.
    - So, undefined behavior.
- Case 2:
    - Helper function:
        - return a "pointer to a heap variable"
    - The veriable is allocated in **Heap**, whose lifetime is *till the end of the project or deleted*.
    - So, it works, but programmer must *delete* manually to avoid *memory leakage*.

- Case 3:  
    - Memory allocation of vector in function:
        ~~~c++
        vector<Type> *vect = new vector<Type>;
        ~~~    
        - With the new operator, **Everything on the free store.**            
    - Helper function:
        - return a "pointer to a heap variable."
    - Like Case 2, it works. 
- Case 4:
    - Memory allocation of vector in function:
        ~~~c++
        vector<Type> vect;
        ~~~
        - **Header info on the stack**. 
        - Elements on the free store (Heap).
    - Helper function:
        - Part stack or?
        - Actually, it is [**move-semantics**](https://stackoverflow.com/questions/15704565/efficient-way-to-return-a-stdvector-in-c) and **named return value optimization (NRVO)**.        
    - Move semantic
        - **local variable** declared in function will be **moved** on return and in some cases even the move can be **elided** by the compiler.
        - Note: *return std::move(vec)* is not preferred because it disable *move-elision* from compiler.
- Case 5: 
    - Like case 4, as long as RAII is followed. Return a local variable is both efficient and safe.
- Case 6:
    - When a function returns a reference, it returns an implicit pointer to its return value.
    - The same as case 1, it fails.

- Note:
    - *Please Note: All C++ containers except *std::array* allocate their memory **dynamically**.*        
    - *std::array* has the same space constraints as C-style arrays do.

## Ref
1. [Stack_Heap_UIUC](https://courses.engr.illinois.edu/cs225/sp2022/resources/stack-heap/)
2. [When vectors are allocated, do they use memory on the heap or the stack?](https://stackoverflow.com/questions/8036474/when-vectors-are-allocated-do-they-use-memory-on-the-heap-or-the-stack)
3. [Efficient way to return a std::vector in C++](https://stackoverflow.com/questions/15704565/efficient-way-to-return-a-stdvector-in-c)
4. [Return Reference to a local variable](https://stackoverflow.com/questions/4643713/c-returning-reference-to-local-variable)