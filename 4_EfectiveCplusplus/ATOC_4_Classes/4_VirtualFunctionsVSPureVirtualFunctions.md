# What is the difference between non-virtual, virtual, and pure virtual functions?
###  Reference: 4.4: virtual function
## Summary
1. non-virtual function
    1. No late-binding, No run-time polymorphism.
2. virtual functions
    1. run-time polymorphism.
    2. When derived class doesn't override, there is a default function.
    3. Base class can be instantiated
3. pure virtual functions
    1. run-time polymorphism.
    2. For interface, force the derived class to override and implement a function.
    3. **Abstract class**: contain at least one pure virtual function.
    4. Base class **cannot** be instantiated

## Detailed information
1. virtual functions v.s. non-virtual functions 
~~~c++
class A {
public:
    void Y() { 
        std::cout << "A" << std::endl; 
    }
    virtual void X() { 
        std::cout << "A" << std::endl; 
    }
};

class B : public A {
public:
    void Y() { 
        std::cout << "B" << std::endl; 
    }
    virtual void X() override 
    { 
        std::cout << "B" << std::endl; 
    }
};

int main() {
  A a; // We can instantiate the class with virtual functions.
  a.Y(); // "A"
  a.X(); // "A"

  B b;
  b.Y(); // "B"
  b.X(); // "B"

  A* ap = &b;
  ap->Y(); // "A", early-binding
  ap->X(); // "B", late-binding at run-time.
}
~~~

2. pure virtual functions v.s. virtual functions.
~~~c++
class Base {
public:
    // pure virtual function.
    virtual void func1() = 0;
};

class Derived : public Base {
public:
    virtual void func1() override {
        cout << "Derived func1\n";
    }
};

int main() {
    // error: cannot declare variable ‘b’ to be of abstract type ‘Base’
    //Base b; 
    Derived d;
    d.func1();
    Base *d2 = new Derived();
    d2->func1();
    return 0;
}
~~~

## Ref:
[1] [Learn C++, The virtual table](https://stackoverflow.com/questions/19086698/whats-the-difference-between-virtual-functions-and-normal-functions)

### Date
2022/06/07