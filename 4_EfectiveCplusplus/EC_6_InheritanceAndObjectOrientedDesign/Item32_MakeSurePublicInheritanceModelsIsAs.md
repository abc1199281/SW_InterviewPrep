# Item 32: Make sure public inheritance model "is-as." = Liskov Substitution Principle

### Reference: Item 32

## Summary
1. "public inheritance" means "is-as." Everything that applies to base classes must also apply to derived classes, because every derived class object is a base class object

2. Liskov Substitution Principle: "public inheritance":
    - Assertion: Every object of type D(derived) is also an object of type B (base).
    - Every D is a B, but not vice versa.

3. Dilema: Penguin is a bird, but Penguin can't fly.
    - Sol: consider "has-as" relationship.

3. meaning of private inheritance: see Item 39.

4. Relationship between classes
    - "is-as": public inheritance
    - "has-a": composition in application domain
    - is-implemented-in-terms-of: 
        - composition in implementation domain
        - private inheritance
        
    
## Detailed Information
- Problem formulation: Penguin is a bird, but Penguin can't fly.
    ~~~c++
    class Bird{
    public:
        virtual void fly();
    };
    class Penguin: public Bird{        
    }
    ~~~
- Work around 1:
    - better and more accurate, 
    - Perfect if there may be no need to distinguish between flying and
non-flying birds.
    ~~~c++
    class Bird{
        // not declare fly function
    };    
    class FlyingBirds: public Bird{        
        virtual void fly();
    }
    class Penguin: public Bird{        
        // not declare fly function
    }
    ~~~

- Work around 2: Penguin can fly, but it's an error.
    - Disadvantage: 
        - Item 18 explains that good interfaces prevent invalid code from compiling.
    ~~~c++
    class Bird{
        virtual void fly();
    };        
    class Penguin: public Bird{        
        virtual void fly(){error("Attempt to make a penguin fly!");}
    };
    ~~~
- Other example: Square and Rectangle
    - If we compromise makeBigger(), we violate Liskov Substitution Principle
    - Consider other relationship, e.g., has-a.
    ~~~c++
    class Rect{/*...*/};
    class Square: public Rect{/*...*/};
    void makeBigger(Rect& r){
        int oldh = r.h();
        r.setW(r.w+10);
        assert(r.h() == oldh);
    }

    Square s;
    makeBigger(s);
    assert(s.w()==s.h()); // Dilemma
    ~~~

### Date
2022/12/29