# What is the Class Invariant (or Invariant)?
###  Reference: 3.5.2: Invariant

## Summary
0. Definition:    
    - A statement of *precondition* that a class (object) should hold throughout its lifetime.
    - Invariant is usually based on *exception handling*, *assertion*, *ctor*, and *dtor*.
1. Solution:
    - Using exception scheme to protect the code.
    ~~~c++
    Vector::Vector(int s){
        
        // This is a class invariant (a.k.a., invariant).
        if (s<0)
            throw length_error{"Vector ctor: neg. size."}

        // remain part
        elem= new double[s];
        sz = s;
    }
    ~~~

### Date
2022/05/22