# What is the Uniform Initialization?

## Simple answer
0. Motivation:
    - Before C++11, initialization methods are different for different types.
    - C++11 tries to unify them.
    - Method: *{} and std::initializer_list*.
1. Sample:
    - before (c++98):
    ~~~c++
    int x1 = 27; // int type with value 27
    int x2(27);  // int type with value 27
    ~~~
    - after (c++11):
    ~~~c++
    int x3= {27}; 
    // type: std::initializer_list<int>
    // value: {27}
    int x4{27};
    // type: std::initializer_list<int>
    // value: {27}
    
    auto x5={1,2,3.0};
    //error! cannot deduce T for 
    // std::initializaer_list<T>
    // Narrowing Initializations.

    int array[]{1,2,3};
    std::vector<int> v{1,2,3};
    std::vector<string> str{
        "a","b","c"
    };


    // std::initializer_list<int> 
    auto ar = {1,2,3};
    ~~~

## Detailed
1. principle:
    - example
    ~~~c++
    std::vector<int> v{2,3,6,7}
    ~~~
    - Fisrt, *.initializer_list()* is a private function which can only called by the compiler.
    ~~~c++
    private: 
        iterator    _M_array;
        size_type   _M_len;

        // The compiler can call a private cotr.
        constexpr initializer_list(const_iterator __a, size_tye __l):_M_array(__a), _M_len(__l){

        }
    ~~~
    - Second, use the object of *std::initializer_list* to initialize *std::vector* with constructor.
    ~~~c++
    vector(initializer_list<value_type> __l,
        const allocator_type & __a = allocator_type()):_Base(__a){
            _M_range_initialize(__l.begin(), __l.end(), random_access_iterator_tag());
        }
    ~~~
2. Initialization without value
~~~c++
int i ;  // i is not defined.
int j{}; // j=0
int *p;  // p is not defined.
int *q{};// q = nullptr.
~~~

## Ref:
[1] [New Feature, uniform initialization](https://www.796t.com/content/1543209674.html)

### Date
2022/05/20