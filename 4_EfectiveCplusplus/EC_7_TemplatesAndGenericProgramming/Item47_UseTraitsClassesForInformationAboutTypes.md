# Item 47: Use Traits classes for information about types

### Reference: Item 47

## Summary
- Traits classes make information about types available during compilation, including pointers.
- They are implemented using templates and template specializations.
- In conjunction with overloading, traits classes make it possible to perform compile-time if...else tests on types.

## Detailed Information
1. Problem Formulation
    1. Example of the need of traits: **std::advance**
        - There are 5 categories of iterators (Appendix 1)
    ~~~c++
    template<typename IterT, typename DistT> // move iter d units
    void advance(IterT& iter, DistT d);      // forward; if d<0, 
                                         // move iter backward.
    ~~~
    2. We'd like utilize the advantage of each category
        - To do so, *We need the information about types during compilation*
    ~~~c++
    template<typename IterT, typename Dist>
    void advance(IterT& iter, DistT d){
        if(iter is a random access iterator){
            iter += d;
        }else{
            if(d>=0){while (d--) ++iter;}
            else{while(d++) --iter;}
        }
    }
    ~~~
2. Traits
    - Motivation: make information about types available during compilation.
    - Properties:
        - Not a keyword or a predefined construct in C++
        - A technique and a convention followed by C++ programmers.
        - Demand: it has to work as *both built-in and user-defined types*, including **pointer**.
        - Built-in type make the nesting information inside type won't do, because there is no way to nest information inside pointers. 
        - That is to say, traits must be **external** to the type.
    - Solution:
        - Implemented as a struct template.
        - A.k.a., **traits classes**.
        - Put it into a template and one or more specializations of that template.        
        ~~~c++
        template<typename IterT> // template for information about
        struct iterator_traits;  // iterator types.
        ~~~
        - For each type *IterT*, a typedef named *iterator_category* is declared in the struct **iterator_traits<IterT>**. This typedef identifies the iterator category of IterT.


3. Example    
    1. imposes the requirement that any used-defined iterator type must contain a nested typedef named *iterator_category* that identifies the appropriate tag struct.    
        - deque
        ~~~c++
        template<...> // template params elided
        class deque{
        public:
            class iterator{
            public:
                typedef random_access_iterator_tag iterator_category;
            };
        };
        ~~~
        - list
        ~~~c++
        template<...>
        class list{
        public:
            class iterator{
                typedef bidirectional_iterator_tag iterator_category;
            };
        };
        ~~~
    2. iterator_traits            
        ~~~c++
        // The iterator_category for type IterT is whatever IterT say it is;
        // see Item 42 for info on the use of "typedef typename".
        template<typename IterT>
        struct iterator_traits{
            typedef typename IterT::iterator_category iterator_category;
        }            
        ~~~
    3. For build-in type
        ~~~c++
        template<typename T>        // partial template specialization
        struct iterator_traits<T*>{ // for build-in pointer types
            typedef random_access_iterator_tag iterator_category; 
        }
        ~~~
    4. Pseudocode for advance:
        - Problem: 
            - We should not if...else on compile time. (before if constexpr() in C++17)
        - Sol:
            - overloading
        ~~~c++
        template<typename IterT, typename DistT>
        void advance(IterT& iter, Dist d){
            if(typeid(typename std::iterator_traits<IterT>::iterator_category)
                ==typeid(std::random_access_iterator_tag)){
                //...
            }
        }
        ~~~
    5. Overloading advance:        
        ~~~c++
        // random access iterators
        template<typename IterT, typename DistT>
        void doAdvance(IterT& iter, Dist d,
                        std::random_access_iterator_tag)  {
            iter+=d;
        }
        template<typename IterT, typename DistT>
        void doAdvance(IterT& iter, Dist d,
                        std::bidirectional_iterator_tag){
            if(d>=0){ while(d--) ++iter;}
            else{while(d++)--iter;}
        }
        template<typename IterT, typename DistT>
        void doAdvance(IterT& iter, DistT d,
                        std::input_iterator_tag){
            if(d<0){
                throw std::out_of_range("Negative distance");
            }
            while(d--)++iter;
        }
        template<typename IterT, typename DistT>
        void advance(IterT& iter, DistT d){
            doAdvance(
                iter, d,
                typename std::iterator_traits<Iter>::iterator_category()
            );
        }
        ~~~
4. Summarization
    1.  Create a set of overloaded "worker" functions or function templates (e.g., doAdvance) that differ in a traits parameter. Implement each function in accord with the traits information passed.
    2.  Create a "master" function or function template (e.g., advance) that calls the worker, passing information provided by a traits class.

## Appendix 1 : Recap of STL 5 categories of iterators
### Ordered by its powerness
1. *input iter*: 
    - move only forward, 
    - 1 step each time,
    - read only
    - access once
    - e.g., istream_iterators (one-pass algorithms)
2. *output iter*:
    - move only forward, 
    - 1 step each time,
    - write only
    - access once
    - e.g., ostream_iterators (one-pass algorithms)
3. forward iter
    - move only forward,
    - write/read more than once (multi-pass algorithms)
    - e.g., single side linked list
4. Bidirectional iter
    - can move backward
5. random access
    - e.g., vector, deque, string

### Tag struct
~~~c++
struct input_iterator_tag{};
struct output_iterator_tag{};
struct forward_iterator_tag: public input_iterator_tag{};
struct bidirectional_iterator_tag: public forward_iterator_tag{};
struct random_access_iterator_tag: public bidirectional_iterator_tag{};
~~~

### Date
2022/12/25