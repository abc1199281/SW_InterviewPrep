# What is the Fold Expression?

### Reference: 7.4.1 fold expression

## Summary
1. Motivation:
    - To simplify the implementation of a simple variadic template, C++17 offers a limited form of iteration over elements of a parameter pack.
2. Example
    ~~~c++
    template<Nunmber...T>
    int sum(T... v){
        // add all elements of v starting with 0.
        return (v+...+0); 
    }

    int x = sum(1,2,3,4,5); // x = 15
    int y = sum('a',2.4,x); // y = 114 (2.4->2, 'a'->97)
    ~~~ 
3. Fold expression:
    - *right fold*:
    ~~~c++
    return (v+...+0);
    // (v[0]+(v[1]+(v[2]+0)))
    ~~~
    - *left fold*:
    ~~~c++
    return (0+...v);
    // (((0+v[0])+v[1])+v[2])
    ~~~

## Detailed Information  
1. Other example: **print**
~~~c++
template<typename ...T>
void print(T&& ... args){
    (std::cout<<...<<args)<<'\n';
}

print("Hello!"s,'a',"World", 2017);
// ((((std::cout<<"Hello!"s)<<'a')<<"World")<<2017<<'\n')
~~~
2. Other example: **to_vector**
~~~c++
template<typename Res, typename...Ts>
vector<Res> to_vector(Ts&&...ts){
    vector<Res> res;
    (res.push_back(ts)...); // no need of initialize value.
    return res;
}

auto x = to_vector<double>(1,2,3,4,5,'a');
~~~

### Date
2022/06/22