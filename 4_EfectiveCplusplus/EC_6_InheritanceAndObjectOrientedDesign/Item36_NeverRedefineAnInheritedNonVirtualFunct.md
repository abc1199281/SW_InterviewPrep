# Item 36: Never redefine an inherited non-virtual function

### Reference: Item 36

## Summary
1. Never redefine an inherited non-virtual function

    
## Detailed Information
- Argument from implementation
    - Controdiction: Same variable, same function, but different behaviors
    ~~~c++
    class B{
    public:
        void mf();
    };
    class D: public B{
        void mf();  // D hides B
    };

    D x;

    B* pB = &x;
    pB->mf();       // mf by B

    D* pD = &x;
    pD->mf();       // mf by D
    ~~~
- Argument theoritically
    1. D is a B. Everything that applies to B also applies to D.
    2. Class derived from B must inherit both the interface and the **implementation**, because D is a B.
    3. (Condroduction) If D modifies the implementation of *mf().*

### Date
2023/01/01