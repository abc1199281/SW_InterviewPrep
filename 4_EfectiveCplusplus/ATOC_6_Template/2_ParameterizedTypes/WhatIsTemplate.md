# What is the Template?

### Reference: 6.1 Introduction Template. 

## Summary
0. High level definition:
    - A **template** is a **class** or a **function** that we parameterize with a set of **types** or **values**.
    - Templates are parameterized by one or more **template parameters**, of three kinds: 
        1. type template parameters
        2. non-type template parameters
        3. template template parameters
1. C++ entity that defines one of the following:
    1. a family of classes (**class template**), which may be nested classes.
    2. a family of functions (**function template**), which may be **member functions**.
    3. an alias to a family of types (**alias template**), (c++11)
    4. a family of variables (**variable template**), (c++14)
    5. a concept (**constraints and concepts**), (c++20)
2. When to use?
    - **Something general** from which we can generate specific **types** and **functions** by specifying arguments, such as *vector*'s element type *double*.
3. When to **Instantiation**, or **specialization**?
    - Compiling time, a.k.a, **instantiation time**.
    - almost no run-time effort.
4. Header-only
    - The definition of a template must be visible at the point of implicit instantiation, which is why template libraries typically provide all template definitions in the headers (e.g. most boost libraries are header-only).

## Detailed Information
1. Parameterized Types
    - Introduction
    - Constrained Template Arguments
    - Value Template Arguments
    - Template Argument Deduction
2. Introduction
~~~c++
template<typename T>
class Vector{
private:
    T* elem;
    int sz;
public:
    // Ctor: Invariant, acquire resources.
    explicit Vector(int s); 
    // Dtor: release resources.
    ~Vector(){delete[] elem;}
    

    // ... copy & move operation

    // for non-const Vector
    T& operator[](int i);  
    // const Vector (4.2.1 ATOC)
    const T& operator[](int i) const; 
    int size() const {return sz;}
};

template<typename T>
Vector<T>::Vector(int s)
{
    // invariant
    if(s<0)
        throw Negative_size{}; 
    elem = new T[s];
    sz = s;
}
template<typename T>
const T& Vector<T>::operator[](int i) const
{
    // invariant
    if(i<0|| size()<=i)
        throw out_of_range{"Vector::operator[]"}; 
    return elem[i];
}

template<typename T> 
T* begin(Vector<T> & x){
    return x.size()? &x[0]:nullptr;
}

template<typename T> 
T* end(Vector<T> & x){
    return x.size()? &x[0]+x.size():nullptr;
}


int main(){
    Vector<char> vc(200);
    Vector<string> vs(17);
    Vector<list<int>> vli(45);

    // Requires .begin(), .end() template functions
    for(auto &s: vs)
        cout<<s<<endl;
}
~~~


### Date
2022/06/06