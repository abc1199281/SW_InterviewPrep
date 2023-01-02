# Item 39: Use private inheritance judiciously

### Reference: Item 39

## Summary
1. Private inheritance menas **is-implemented-in-terms of**.
    - That is, purely an implementation technique.    
    - There is no conceptual relationship between D and B.
    - Only *implementation* is inherited, but *interface* is ignored.
2. It is *usually inferior* to composition, but it make sense when a derived class 
    - needs access to protected base class members, or
    - needs to redefine inherited virtual functions.
    - Basically, use Composition whenever you can, and use private inheritance whenever you must.
3. Unlike composition, private inheritance can enable the **empty base optimization (EBO).**
    - This can be important for library developers who strive to minimize object size.

## Detailed Information
- Recap Item 32:
    ~~~c++
    class Person{/*...*/};
    class Student: private Person{/*...*/}; // Become private
    ~~~
- 2 Rules (Behaviors) of Private Inheritance:
    1. Compiler not convert a derived class object into a base class object.
        ~~~c++
        void eat(const Person& p);        
        Student s;    
        eat(s); // Error! A student isn't a Person
        ~~~
    2. members inherited from a private base class become private members of the derived class, even if they were protected or pubic in the base class.
- Meaning of Private Inheritance:
    - Private inheritance is **purely an implementation technique**
    - You are interested in taking advantage of some of the features available in class B.    
    - **Not** because there is any conceptual relationship between D and B.

- Scenario that might use private inheritance
    - Given *Widgets*, 
        - we need to counter the utilisations periodically, 
        - some modification is required.
    - Given *Timer*
    ~~~c++
    class Timer{
    public:
        explicit Timer(int tickFrequency);  // We can assign the freq.
        virtual void onTick() const;        // We can redefine to examines Widget.
    };
    ~~~

- Solution 1: private inheritance
    - Why not public?
        - *onTick* should not be an interface, which might be used by clients.
    - Essential meaning:
        - is implemented in terms of: Timer
    - Limitations:
        1. Derived classes of Widget, we cannot stop them from redefine onTick().
            - like *final* in Java
        2. Reduce dependency
            - Inheritance: Definition must be accessible.
            - Composition: forward declaration  is enough.
    ~~~c++
    class Widget: private Timer{
    private:
        virtual void onTick() const;        // Examines Widget's data.
    }
    ~~~
- Solution 2: Still use composition and public inheritance
    ~~~c++
    class Widget{
    private:
        class WidgetTimer: public Timer{
        public:
            virtual void onTick() const;
        };
        WidgetTimer timer;
    };
    ~~~

- Edge case: **Empty base optimization, (EBO)**
    - Only if size is really important.
    - Default non-zero size:
        - sizeof(HoldsAnInt)>sizeof(int);
        - compiler assign *char* in default, or alignment (padding to int).
        ~~~c++
        class Empty{/*
        - typedefs, 
        - enums, 
        - static, 
        - non-virtual functions
        */};

        class HoldsAnInt{
        private:
            int x;
            Empty e;
        };
        ~~~
    - Solution:
        - sizeof(HoldsAnInt) = sizeof(int);
        ~~~c++
        class Empty{};

        class HoldsAnInt: private Empty{
        private:
            int x;
        }
        ~~~
    - example of empty base class
        - classes unary_function
        - classes binary_function
    


### Date
2023/01/01