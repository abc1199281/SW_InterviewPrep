# What is the Generic Programming?

### Reference: 7.3.1 fold expression

## Summary
1. Motivation:
    - The form of **generic programming** centers around the idea of abstracting from concrete, efficient algorithms to obtain generic algorithms.
    - **concepts**: Abstractions represent the fundamental operations and data structures.

## Detailed Information  
### Abstraction Using Template

1. Good abstractions are carefully grown from concrete examples.
    - start with concrete examples from real use and try to eliminate inessential details.

    ~~~c++
    double sum(const vector<int>&v){
        double res = 0;
        for(auto x:v)
            res+=x;
        return res;
    }
    ~~~

2. Questions
    1. Why just ints?
    2. Why just vectors?
    3. Why accumulate in a double?
    4. Why start at 0?
    5. Why add?

3. Q1-Q4:  
    - **lifting**: The process of generalizing from a concrete piece of code while preserving performance.
    ~~~c++
    template<typename Iter, typename Val>
    Val accumulate(Iter first, Iter last, Val res){
        for(auto p = first; p!=last;++p)
            res+=*p;
        return res;
    }

    void use(const vector<int>& vec, const list<double>& lst){
        // add to a double, across vec and lst using the same function.
        auto sum = accumulate(begin(vec), end(vec),0.0);
        auto sum2 = accumulate(begin(lst), end(lst),sum); 
    }
    ~~~
    
4. Get rid of begin() and end()
    ~~~c++
    // a Range is something with begin() and end().
    template<Range R, Number Val> 
    Val accumulate(const R&r, Val res = 0){
        for(auto p = begin(r), p!=end(r);++p)
            res +=*p;
        return res;
    }
    ~~~

### Date
2022/06/25