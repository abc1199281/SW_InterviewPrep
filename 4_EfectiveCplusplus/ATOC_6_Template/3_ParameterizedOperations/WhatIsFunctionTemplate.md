# What is the Function Template?

### Reference: 6. 3 Parameterized operation

## Summary
0. Sample :
    - simplified version of *std::accumulate()*.
    ~~~c++
    template<typename Sequence, typename Value>
    Value sum(const Sequence & s, Value v){
        for(auto x:s)
            v+=x;
        return v;
    }

    // usage
    int x = sum(vi, 0);
    ~~~
1. Note:
    - *Function template* can be member function.
    - Function template cannot be *virtual function*,
        - because virtual function utilize *late-binding*, or run-time selection
        - template instantiate in *compile-time*.


## Detailed Information
1. Parameterized Operations
    - **Function template**
    - Function object: 
        - an object that can carry data and be called like a function
    - Labda expression
        - a shorthand notation for a function object.

### Date
2022/06/11