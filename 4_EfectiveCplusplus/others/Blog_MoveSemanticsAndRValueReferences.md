# Move semantics and rvalue references in C++11

## Summary
0. Motivation:
    - Until C++11, there has been an obstinate wart that slows down many c++ program.
        - **the creation of temporary objects.**
    - Solution: **move semantics**, which rely on **rvalue reference**
    
1. Rvalues and Lvalues
    - lvalues: an expression whose address can be taken, including function
    - rvalues: temporary objects

2. Detecting temporary objects with rvalue reference    
    - *An **rvalue reference** is a  **reference (a lvalue)** that will **bind "only" to a temporary object**.*
    - How does it help? --> **Rvalue reference version method** is like the secret back door entrance to the club that **you can only get into if you're a temporary object**. 

3. Move constructor and move assignment operator
    - rather than allocate and initialize new memory, **we can simply steal the pointer and null out the pointer in the temporary object! We know the temporary object will no longer be needed**, so we can take its pointer out from under it.
    - Whole point of a move ctor: **to avoid a copy by changing the original, temporary object!**
    - **Both lvalue and rvalue references are lvalue expressions**.

4. std::move:
    - Because **Rvalue reference version method** only accept temporary object.
    - Sometime, we may say "ok, honest to God I know I have an lvalue, but I want it to be an rvalue."


## Detailed Information
### 0. Motivation:
- until C++11, there has been an obstinate wart that slows down many c++ program.
    - the creation of temporary objects.
    - sometime, compiler helps, but not always the case.
~~~c++
#include <iostream>
using namespace std;

vector<int> doubleValues(const vector<int> & v)
{
    vector<int> new_values;
    new_values.reserve(v.size());
    for(auto itr = v.begin(), end_itr = v.end(); itr!=end_itr; ++itr){
        new_values.push_back(2* *itr);
    }
    return new_values;
}
int main()
{
    vector<int> v;
    for(int i = 0;i<100;i++){
        v.push_back(i);
    }
    v = doubleValues(v);
}
~~~
- Description
    - Terrible C++03 code, but fine c++11 code.
    - what happened in return? 2 copies in C++03
        1. one into a temporary object to be returned. (compiler can help)
        2. second when vector assignment operator runs on v = doubleValues(v);
    - The worst part: **after copy, variable is thrown away immediately. Why not move**
        - C++03: no way to tell if an object was a temporary or not.
        - C++11: Yes, you can!
            - That's what **rvalue reference**, and **move semantics** are for!
            - move semantics rely on rvalue reference
    

### 1. Rvalues and Lvalues - bitter rivals, or best of friends?
- lvalues: an expression whose address can be taken, including function
~~~c++
int x; 
int & getRef(){
    return x;
}
getRef() = 4; // lvalue

int getVal(){
    return x;
}
getVal(); // rvalue, temporary value
~~~

### 2. Detecting temporary objects with rvalue reference
- Introduction
    - **rvalues refer to temporary objects.**
    - Can we know that a value returned from an express was temporary?
        - And write code to work more efficient?
        - That's why **rvalue reference** are for.
    - *An **rvalue reference** is a reference that will **bind only to a temporary object**.*
- Historic recall (prior to C++11):
    - If you had a **const** temporary object, you could use a "regular" or "lvalue reference" to bind it.
    - You cannot use a "mutable" reference
    ~~~c++
    const string& name = getName();// ok
    string& name = getName(); // NOT ok
    ~~~
- In C++11:
    - new reference: "rvalue reference", let you bind a muitable reference to an rvalue, but not an lvalue.
    - In other words, **rvalue references (&&) are perfect for detecting if a value is temporary object or not.**
    - can be const and non-const, just like lvalue references
    ~~~c++
    const string&& name = getName(); // ok
    string&& name = getName(); // also ok - praise be!
    ~~~
    
- **But how does it help?** The most important thing about rvalue references vs lvalue references is what happens when you write functions that take lvalue or rvalue references as parameters.
    ~~~c++
    void printReference(const String& str){ // A
        cout<<str;
    }
    void printReference(string&& str){ // B
        cout << str;
    }
    string me("alex");
    printReference(me); // calls A, taking an lvalue reference
    printReference(getName()); // call B, taking a mutable rvalue reference
    ~~~
- **Rvalue reference version method** is like the secret back door entrance to the club that **you can only get into if you're a temporary object**. 

### 3. Move constructor and move assignment operator
- Introduction
    - most common pattern with rvalue references: move ctor and move assignment.
    - move ctor can avoid memory reallocation because we know it has been provided a temporary object.

- What does it mean to move a field of the object?
    - primitive type: we just copy
    - pointer: 
        - rather than allocate and initialize new memory, **we can simply steal the pointer and null out the pointer in the temporary object! We know the temporary object will no longer be needed**, so we can take its pointer out from under it.
    ~~~c++
    class ArrayWrapper
    {
        public:
            ArrayWrapper(int n): _p_vals(new int[n]), _size(n){}

            // copy ctor
            ArrayWrapper(const ArrayWrapper& other): _p_vals(new int[other._size]), _size(other._size){
                for(int i = 0;i<_size;i++){
                    _p_vals[i] = other._p_vals[i];
                }
            }

            // move ctor, steal the address in the temporary pointer.
            ArrayWrapper (ArrayWrapper && other): _p_vals(other._p_vals), _size(other.size)
            {
                other._p_vals = NULL;
                other._size = 0;
            }

            ~ArrayWrapper(){
                delete [] _p_vals;
            }
        private:
        int *_p_vals;
        int _size;
    };
    ~~~
    - Move ctor:
        1. The parameter is a non-const rvalue reference
        2. otehr._p_vals is set to NULL
    - We couldn't set otehr._p_vals to NULL if we'd taken a const rvalue reference.
    - Why we need to set? The reason is the destructor.
        - When the temporary object goes out of scope, the desctructor will run.
    - **Whole point of a move ctor: to avoid a copy by changing the original, temporary object!**
    - Currently, the overload rules only work for **non-const temporary**, so, don't write member function like this
    ~~~c++
    const ArrayWrapper getArrayWrapper(); // make move ctor useless, temporary is const!
    ~~~
    - How to handle in the move ctor? 
        - e.g., complex metadata?
    ~~~c++
    class MetaData{
    public:
        MetaData(int size, const std::string& name)
            : _name(name)
            , _size(size)
        {}

        // copy ctor
        MetaData(const MetaData& other)
            : _name(other._name)
            , _size(other._size)
        {}

        // move ctor
        MetaData(const MetaData&& other)
            : _name(other._name)
            , _size(other._size)
        {}

        std::string getName() const {return _name;}
        int getSize() const {return _size;}
    private:
        std::string _name;
        int _size;
    }
    class ArrayWrapper
    {
        public:
            ArrayWrapper(int n) 
                : _p_vals(new int[n])
                , _metadata(n, "ArrayWrapper"){}

            // copy ctor
            ArrayWrapper(const ArrayWrapper& other)
                : _p_vals(new int[other._metadata.getSize()])
                , _metadata(other._metadata){
                for(int i = 0;i<_size;i++){
                    _p_vals[i] = other._p_vals[i];
                }
            }

            // move ctor
            ArrayWrapper (ArrayWrapper && other)
                : _p_vals(other._p_vals)
                , _metadata(other._metadata)
            {
                // if _metadata(other._metadata) calls the move constructor in metadata, 
                // using other._metadata here would be extremely dangerous!!
                other._p_vals = NULL;                
            }

            ~ArrayWrapper(){
                delete [] _p_vals;
            }
        private:
        int *_p_vals;
        MetaData _metadata;
    };
    ~~~

    - Does it work? No
        - The value of other in the move ctor, it's an rvalue reference.
        - rvalue reference is not an rvalue, and so the copy ctor is called.
        - we might use the variable other more than once in the function.
    - **Both lvalue and rvalue references are lvalue expressions**.
        - lvalue reference must be const to hold a reference to an rvalue.
        - rvalue reference can always hold a reference to an rvalue.
        - Like: a pointer v.s. what is pointed to.
        - The thing pointed-to came from an rvalue, but when we use rvalue reference itself, it results in an lvalue.

### 4. std::move
- Introduction
    - The trick to handle the case.
    - <utility> -- std::move:
        - "ok, honest to God I know I have an lvalue, but I want it to be an rvalue."
        - std::move does not move anything; it just turns an lvalue to rvalue.
    
    ~~~c++
    // ArrayWrapper:: move ctor
    ArrayWrapper (ArrayWrapper&& other)
        : _p_val( other._p_vals)
        , _metadata(std::move( other._metadata))
        {
            other._p_vals = NULL;
        }
    
    // MetaData:: move ctor
    Metadata (MetaData&& other)
        : _name(std::move(other._name)) // oh. blissful efficiency
        , _size(other._size)
        {}
    ~~~
    - How it works?
        - typcasting, static_cast to an rvalue reference.
        - You must explicitly use std::move to convert an lvalue into an rvalue reference, and rvalue reference will never bind to an lvalue on its own. 

### 5. Returning an explicit rvalue-reference from a function
- Are there ever times where you should write a function that returns an rvalue reference? what does it mean? Aren't functions that return objects by value already rvalues?
- Do you need to do this? probably not. In most cases, it just makes it more likely that you'll end up with dangling reference, like the danger of returning an lvalue reference.
~~~c++
int x;
int getInt()
{
    return x;
}

int && getRvalueInt()
{
    // notice that it's fin to move a primitive type -- remember, std::move is just a cast
    return std::move(x);
}

void printAddress(const int& v){
    cout << reinterpret_cast<const void*>(&v)<<endl;
}

// two separate values
printAddress(getInt());
printAddress(x);

// two same values
printAddress(getRvalueInt());
printAddress(x);
~~~

## Ref:
[1] [Move semantics and rvalue references in C++11
](https://www.cprogramming.com/c++11/rvalue-references-and-move-semantics-in-c++11.html)

### Date
2022/12/03