# Item 18: Make interfaces easy to use correctly and hard to use incorrectly

### Reference: Item 18

## Introduction
- correctness
- efficiency
- encapsulation
- maintainability
- extensibility
- *conformance to convention*
    - One of the most important property to make interface easy to use.

## Summary
- Good interfaces are easy to use correctly and hard to use incorrectly.
    - You should strive for these characteristics in all yuor interfaces.        
- Ways to facilitate correct use include 
    - consistency in interfaces, 
    - and behavioral compatibility with build-in types.

- Ways to prevent errors include 
    - creating new types, 
    - restricting operations on types, 
    - constraining object values, 
    - and elmiminating client resource management responsibilities.

- std::shared_ptr supports custom deleters. 
    - This prevents the cross DLL proglem, can be used to automatically unlock mutexes (see Item 14), etc.

## Detailed Information
1. Example: Creating new types & Rrestricting operations on types
    - Original design:            
        ~~~c++
        class Date{
        public:
            Date(int month, int day, int year);
        }
        ~~~
        - Risk:
        ~~~c++
        Date d(30, 3, 1995); // UK format

        Date d(2, 30, 1995); // over range
        ~~~ 
    - Major solution: Type system, Wrapper Types
        - Note: It is only for example. classes are usually better.
        ~~~c++
        struct Day{
            explicit Day(int d): val(d){}
            int val;
        };
        struct Month{
            explicit Month(int d): val(d){}
            int val;
        };
        struct Year{
            explicit Year(int d): val(d){}
            int val;
        };
        class Date{
        public:
            Date(const Month& m, const Day& d, const Year& y);
        };

        Date d(30, 3, 1995);                    // error, incorrect type
        Date d(Day(30), Month(3), Year(1995));  //error! incorrect type
        Date d(Month(3), Day(30), Year(1995));
        ~~~
2. Example: Constraining object values
    - One way: enum
        - limitation: enums are not as type-safe as we might like. For example, enums can be used like ints
    - Safer solution is to predefine the set of all valid Months
    ~~~c++
    class Month{
    public:
        static Month Jan(){return Month(1);}
        static Month Feb(){return Month(2);}
        //...
        static Month Dec(){return Month(12);}
    private:
        explicit Month(int m);
    };
    Date d(Monthe::Mar(), Day(30), Year(1995));
    ~~~
3. Example: Elmiminating client resource management responsibilities.
    - Problem formulation
        - Any interface that requires that clients remember to do something is prone to incorrect use.
        - Risk of resource leaks
        ~~~c++
        Investment* createInvestment(); // from Item 13
        ~~~
    - Basic solution:
        ~~~c++
        std::shared_ptr<Investment> createInvestment();
        ~~~
    - Extend problem:
        - Suppose clients are expected to use *getRidOfInvestment()* instead of *delete*. 
            - We open the door to a new kind of client error.
        - Solution:
            ~~~c++
            std::shared_ptr<Investment> createInvestment(){
                std::shared_ptr<Investment> retVal(static_cast<Invextment*>(0),
                                             getRidOfInvestment);
                // retVal = 
                return retVal;
            }
            ~~~


### Date
2023/01/03