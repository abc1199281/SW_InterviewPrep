# Item 35: Consider alternatives to virtual functions

### Reference: Item 35

## Summary
- The fundamental advice of this Item is to consider alternatives to virtual functions when searching for a design for the problem you're trying to solve.
    1. Use the **non-virtual interface idiom (NVI idiom)**, a form of the **Template Method** design pattern that wraps public non-virtual member functions around less accessible virtual functions.
    2. Replace virtual functions with **function pointer data members,** a stripped-down manifestation of the **Strategy** design pattern.
    3. Replace virtual functions with **std::function data members,** thus allowing use of any callable entity with a signature compatible with what you need. This, too, is a form of the **Strategy** design pattern.
    4. Replace virtual functions in one hierarchy with **virtual functions in another hierarchy.** This is the conventional implementation of the Strategy design pattern.


## Things to Remember
- Alternatives to virtual functions include the **NVI idiom** and various forms of the **Strategy** design pattern. The **NVI idiom** is itself an example of the **Template Method** design pattern.
- A disadvantage of moving functionality from a member function to a function outside the class is that the non-member function lacks access to the class's non-public members.
- std::function objects act like generalized function pointers. Such objects support all callable entities compatible with a given target signature.
    
## Detailed Information
- Problem formulation:
    - We are designing a hierarchy for characters in the game.
    - A member function, healthValue, is added.    
    - Other alternatives?
    ~~~c++
    class GameCharacter{
    public:
        virtual int healthValue() const;        
    };
    ~~~

- Alternative 1: Template Method via Non-virtual Interface Idiom (NVI)    
    - Motivation: Non-virtual Interface (NVI), healthValue(), a wrapper.
    - Pros:
        - Do before/after: Setting up proper context
            - e.g., log entry / locking a mutex, etc.
            - If clients can use this functions direcly,
            - context would be in the virtual function.
        - Base class:   
            - Calling a virtual function specifies *when* it will be done.
            - Reverses for itself the right to *say when* the function will be called.        
        - Derived class:
            - Redefine a virtual function specifies *how* something is to be done.
            - Give them control over *how* functionality is implemented.
    - Cons (Limits):
        - Cannot have a per-object health calculation functions.
        - No change such functions at run-time.
    ~~~c++
    class Game Character{
    public:
        int healthValue() const{            // derived class do not redefine 
                                            // it, see Item 36.
            //...                           // do "before" stuff - see below
            int retVal = doHealthValue();   // do the real work            
            //...                           // do "after" stuff - see below
            return retVal;
        }
    private:
        virtual int doHealthValue() const{  // derived classes may redefine this
            //...                           // default algorithm
        }
    };
    ~~~

- Alternative 2: Strategy Pattern via Function Pointers
    - Pros:
        - ability to have a per-object health calculation functions.
        - ability to change such functions at run-time.
    - Cons: Decreased encapsulation
        - Health calculation function has no special access to the internal parts, unless public access functions are provided.
    
    ~~~c++
    class GameCharacter; // forward declaration
    int defaultHealthCalc(const GameCharacter& gc);

    class GameCharacter{
    public:
        typedef int (*HealthCalcFunc) (const GameCharacter&);
        explicit GameCharacter(HealthCalcFunc hcf = defaultHealthCalc)
        : healthFunc(hcf)
        {}
        int healthValue() const
        { return healthFunc(*this);}
    private:
        HealthCalcFunc healthFunc;
    };
    ~~~
    - Interesting flexibility:
        1. Same character type can have different health calculation functions
        ~~~c++
        class EvilBadGuy:public GameCharacter{
        public:
            explicit EvilBadGuy(HealthCalcFunc hcf = defaultHealthCalc)
            :GameCharacter(hcf)
            {/*...*/}
        };

        int loseHealthQuickly(const GameCharacter&); // health calculation
        int loseHealthSlowly(const GameCharacter&);  // funct.s with different
                                                     // behavior

        EvilBadGuy ebg1(loseHealthQuickly);          // same-type characters
        EvilBadGuy ebg2(loseHealthSlowly);           // with different 
                                                     // health-related behaviors
        ~~~
        2. Health calculation functions for a particular character may be changed at runtime. e.g., *setHealthCalculator.*

- Alternative 3: Strategy pattern via std::function
    - Motivation:
        1. Why can't it be a member function?
        2. Why must health calculator be a function instead of simply something that *acts* like a function (e.g., a function object)?
        3. Why must it return an int instead of any type convertible to an int?
    - std::function in C++
    ~~~c++
    class GameCharacter;
    int defaultHealthCalc(const GameCharacter& gc);
    class GameCharacter{
    public:
        // HealthCalcFunc is any callable entity that meets target signature.
        typedef std::function<int(const GameCharacter&)> HealthCalcFunc;      
        explicit GameCharacter(HealthCalcFunc hcf = defaultHealthCalc)
        : healthFunc(hcf)
        {}
        int healthValue() const
        { return healthFunc(*this);}
    private:
        HealthCalcFunc healthFunc;
    };
    ~~~
    - "target signature": *int (const GameCharacter&)*
        ~~~c++
        std::function<int (const GameCharacter&)>
        ~~~
        - Q1: GameCharacter now hold a generalized function pointer as member variable.
        - Q3: Types can be implicitly converted.
    - Q2: More flexibility in specifying health calculation functions
    ~~~c++
    short calcHealth(const GameCharacter&); // HCF: note, non-int return type

    struct HealthCalculator{                // class for HCF function objects
        int operator()(const GameCharacter&) const
        {/*...*/}; 
    };

    class GameLevel{
    public:
        // HCF: note, non-int return type
        float health(const GameCharacter&) const; 
    };

    class EvilBadGuy: public GameCharacter{// as before        
    };

    class EyeCandyCharacter: public GameCharacter{        
    };

    EvilBadGuy dbg1(calcHealth);

    EyeCandyCharacter ecc1(HealthCalculator());

    GameLevel currentLevel;

    EvilBadGuy ebg2(
        std::bind(&GameLevel::health,   // character using a 
                  currentLevel,         // HCF;
                _1);                    //
    )
    ~~~
    - Detailed explaination:
        - In fact, *GameLevel::health* have two params 
            1. this->
            2. const GameCharacter&
        - But, HCF only accept *const GameCharacter&*.
        - Conversion: **std::bind**
            - std::bind(&GameLevel::health, currentLevel, _1);
    - by using std::function instead of a function pointer, we’re allowing clients to use **any compatible callable entity** when calculating a character’s health.

- Alternative 4: The "Classic" Strategy Pattern
    - GameCharacter:
        - Derived class: EvilBadGuy, EyeCandyCharacter
        - Composition: HealthCalcFunc
    - HealthCalcFunc
        - Derived class: SlowHealthLoser, FastHealthLoser
    ~~~c++
    class GameCharacter;
    class HealthCalcFunc{
    public:
        virtual int calc(const GameCharacter& gc) const
        {/*...*/}
    };

    HealthCalcFunc defaultHealthCalc;

    class GameCharacter{
    public:
        explicit GameCharacter(HealthCalcFunc* phcf = &defaultHealthCalc)
        :publicCalc(phcf)
        {}
        int healthValue() const
        { return pHealthCalc->calc(*this);}
    private:
        HealthCalcFunc* pHealthCalc;
    };
    ~~~

### Date
2022/12/29