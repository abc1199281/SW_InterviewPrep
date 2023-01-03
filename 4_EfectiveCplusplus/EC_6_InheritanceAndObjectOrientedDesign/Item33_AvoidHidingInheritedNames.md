# Item 33: Avoid hiding inherited names

### Reference: Item 33

## Summary
1. Name in derived classes hide names in base classes. Under public inheritance, this is never desirable.
2. To make hidden names visible again, employ using declarations or forwarding functions.
    
## Detailed Information
- Problem formulation: Scope
    - Name-hiding rules
    ~~~c++
    int x;
    void someFunc(){
        double x;
        std::cin>>x;
    }
    ~~~

    - Enter Inheritance.
        - We are talking about *name*. 
        - Functions types do not matter.
    ~~~c++
    class Base{
    private:
        int x;
    public:
        virtual void mf1() = 0; 
        // not inherited if same name exist in D, although different args.
        virtual void mf1(int ); 
        virtual void mf2();
        void mf3();
        // not inherited if same name exist in D, although different args.
        void mf3(double);
    };
    class Derived: public Base{
    public:
        virtual void mf1(); // hide B::mf1(int)
        void mf3();// hide B::mf3(int)
        void mf4;
    }
    ~~~
- Solution: using (public inheritance)
    ~~~c++
    class Base{
    private:
        int x;
    public:
        virtual void mf1() = 0; 
        // now inherited.
        virtual void mf1(int ); 
        virtual void mf2();
        void mf3();
        // now inherited.
        void mf3(double);
    };
    class Derived: public Base{
    public:
        using Base::mf1;
        using Base::mf3;
        virtual void mf1(); 
        void mf3();
        void mf4;
    }
    ~~~
- Solution: forwarding function (private inheritance)
    ~~~c++
    class Derived: private Base{
    public:
        virtual void mf1(){Base::mf1();}; 
        void mf3();
        void mf4;
    }
    ~~~

### Date
2022/12/29