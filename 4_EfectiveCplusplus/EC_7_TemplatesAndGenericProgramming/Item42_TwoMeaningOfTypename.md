# What is the two meaning of typename?

### Reference: Item 42 

## Summary
1. When declaring template parameters, class and typename are interchangeable.
~~~c++
template<class T> class Widget;
template<typename T>class Widget;
~~~
2. Use typename to identify **nested dependent type names**, except in base class lists or as a base class identifier in a member initialization list.


## Detailed Information
- There are **two** kinds of name you can refer in a template.
    - dependent names
    - non-dependent names
    ~~~c++
    // example, not compliable
    template<typename C>
    void print2nd(const C& container){
        if (container.size() >=2){
            C::const_iterator iter(container.begin()); 
            // iter: dependent name, .
            // more precisely, nested dependent type name.

            ++iter;
            int value = *iter; // value: non-dependent name
            std::cout << value;
        }
    }
    ~~~
- Motivation: nested dependent name can lead to parsing difficulties.
    ~~~c++
    template<typename C>
    void print2nd(const C& container){
        C::const_iterator *x; 
        // const_iterator might be a variable or a type
    }
    ~~~
- Solution: 
    - rule: parser assumes that the name is not a type unless you tell it otherwise.    
    
    ~~~c++
    template<typename C>
    void print2nd(const C& container){
        typename C::const_iterator iter(container.begin()); 
        // const_iterator might be a variable or a type        
    }
    ~~~





## Ref:

### Date
2022/12/07