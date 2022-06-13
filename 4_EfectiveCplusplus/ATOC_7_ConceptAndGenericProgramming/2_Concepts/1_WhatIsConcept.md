# What is a concept (C++20)?

### Reference: 7.2 concept

## Summary
1. Motivation:
    - Type checking with meaningful error message in template
    - Like assembly code, low level code.
2. Sample of Motivation:
    ~~~c++
    template<typename T>
    auto sum(T t1, T t2){
        return t1+t2;
    }

    struct S{};
    S s1, s2;
    cout<<sum(s1,s2)<<endl;// error.
    ~~~ 
3. Sample Solution:
    - a new template called *concept*.
    - We declare variable: *addable*.
    - When expression is legal, return true. Else, return false.
    - Note, there is no calculation.
    - *syntactic and semantic requirements*
    ~~~c++
    template<typename T>
    concept addable = requires(T a, T b){
        a+b;
    };

    template<typename T>
    auto sum(T t1, T t2) requires addable<T>{
        return t1+t2;
    }
    ~~~

## Detailed Information
1. atomic constraint
    - RHS: compile-time calculation true or false.
    ~~~c++
    template<typename T, typename U>
    concept is_same_as = std::is_same_v<T,U>;
    ~~~
2. Conjunctions
    ~~~c++
    template<T>
    concept Integral = std::is_integral<T>::value;
    template<T>
    concept SignedIntegral = Integral<T>&& std::is_signed<T>::value;
    ~~~
3. Type of concepts
    - core language concepts
        - same_as
        - derived_from
        - integral
        - floating_point
        - swappable
        - move_constructible        
    - Comparison 
        - three_way_comparable
    - Object
        - movable
        - copyable
        - regular
    - Callable concept
        - predicate
4. Overloading
    ~~~c++
    template<Forward_iterator Iter>
    void advance(Iter p, int n){
        while(n--)
            ++p;
    }

    template<Random_access_iterator Iter>
    void advance(Iter p, int n){
        p+=n;
    }

    void user(vector<int>::iterator vip, 
              list<string>::iterator lsp){
        advance(vip, 10);
        advance(lsp, 10);
    }
    ~~~
5. Requires expressions
    ~~~c++
    // require expression
    template<typename T>
    concept Addable = requires(T x){x+x;};

    // requires-clause, not require expression
    template<typename T> requires Addable<T>
    T add(T a, T b){
        return a+b;
    }

    // ad-hoc constraint, note keyword used twice.
    template<typename T>
        requires requires T(x){x+x;}
    T add(T a, T b){return a+b;}
    ~~~
6. Another sample: Equality_comparable
    ~~~c++
    template<typename T>
    concept Equality_comparable = 
        requires(T a, T b){
            {a==b}->bool;
            {a!=b}->bool;
        }

    struct S{int a;};
    static_assert(Equality_comparable<int>)//OK
    static_assert(Equality_comparable<S>)//fails
    ~~~
7. Another sample: Sequence
    ~~~c++
    template<typename S>
    concept Sequence = requires(S a){
        typename Value_type<S>;
        typename Iterator_type<S>;

        {begin(a)}->Iterator_type<S>;
        {end(a)}->Iterator_type<S>;

        requires Same_type<Value_type<S>, Value_type<Iterator_type<S>>>;
        requires Input_iterator<Iterator_type<S>>;
    }
    ~~~
### Ref
[1] [Jonny's blog: 【C++ 20】Concept](https://jonny.vip/2021/07/11/%e3%80%90cplusplus-20%e3%80%91concept/)

### Date
2022/06/12