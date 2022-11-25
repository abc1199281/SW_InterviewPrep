# What is the variadic template?

### Reference: 7.4 variadic template

## Summary
1. Definition:
    - A template can be defined to accept an arbitrary number of arguments of arbitrary types.
    - Usage: recurrence.
    
2. Sample of Motivation:
    ~~~c++
    // usage
    void user(){
        print("first: ",1,2.2,"hello");
    }

    // when there is no argument, do nothing.
    // base condition.
    void print(){

    }

    // what we do for each argument.
    template<typename T, typename... Tail>
    void print(T head, Tail... tail){
        cout<<head;
        print(tail...);
    }
    ~~~ 
3. Sample Solution:
    - *typename... Tail*
        - Tails is a sequence of types.
        - Parameter declared with *...* is **parameter pack**.    
4. Cons:
    - The recursive implementation can by tricky to get right.
    - The recursive implementation can be suprisingly expensive in compile time.
    - The type of checking of the interface is a possibly elaborate template program.

## Detailed Information
1. Another version for base condition
~~~c++
template<typename T, typename... Tail>
void print(T head, Tail... tail)
{
    cout<<head;
    if constexpr(sizeof...(tail)>0)
        print(tail...);
}
~~~

### Date
2022/06/16