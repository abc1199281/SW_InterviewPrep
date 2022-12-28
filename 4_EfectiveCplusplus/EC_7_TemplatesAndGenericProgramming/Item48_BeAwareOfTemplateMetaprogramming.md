# Item 48: Be aware of Templat metaprogramming

### Reference: Item 48

## Summary
- Template Metaprogramming is Turing-complete and functional language.
- Loop in Template is often implemented as recursion.
- Template Metaprogramming can shift work from runtime to compile-time, thus enabling earlier error detection and higher runtime performance.
- TMP can be used to generate custom code based on combinations of policy choices, and it can also be used to avoid generating code in appropriate for particular types.
- TMP will probably never be main-stream, but for some programmers - especially library developers - it's almost certain to be a staple.

## Detailed Information
1. Two strength
    1. it makes some things easy that would otherwise be hard or impossible.
    2. shift work from run-time to compile time.
    - e.g., advance
    ~~~c++
    // type id based solution: lower performance
    template<typename IterT, typename DistT>
    void advance(IterT& iter, DistT d)
    {
        if(typeid(typename std::iterator_traits<IterT>::iterator_category)
            == typeid(std::random_access_iterator_tag)){
            iter += d;
        }else{
            if(d>=0){while(d--)++iter;}
            else{while(d++)--iter;}
        }
    }
    ~~~
    - reason: 
        - run-time checking type and code size.
        - Might still error when compiler instantiate type
        ~~~c++
        void advance(std::list<int>::iterator& iter, int d){
            if(typeid(std::iterator_traits<std::list<int>::iterator>::iterator_category)
            ==...){
                // still induce compiler error, because compiler check every operation in the functions
                iter+=d;
            }else{
                //...
            }            
        }
        ~~~
2. Factorial template
    - 
    ~~~c++
    template<unsigned n>
    struct Factorial{
        enum{value = n*Factorial<n-1>::value};
    };
    template<>
    struct Factorial<0>{
        enum{value = 1};
    };
    int c = Factorial<5>::value;
    ~~~
3. Example of advantages
    1. Earlier correction (during compilation)
    2. Expression templates
        - Original: 4 temperary matrix are created.
        - Expression templates: eliminate temperary matrix.
            - Less memory, dramatically  enhance speed.
        ~~~c++
        BigMatrix result = m1*m2*m3*m4*m5;
        ~~~
    3. Design pattern
        - Strategy, Observer, Visitor
            - Policy-based design (TMP-based)
            - e.g., smart pointer (behavioral policies)
            - generative programming
### Date
2022/12/25