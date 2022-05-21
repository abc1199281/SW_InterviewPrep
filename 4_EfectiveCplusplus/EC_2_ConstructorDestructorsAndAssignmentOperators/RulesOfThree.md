# What is the Rules of Three in C++?

## Summary
0. Motivation:
    - Simple and Effective Rule for Resource (memory) management in OOP).    
    - Avoid memory reallocation or twice releasing.
1. Rules of three
    - There are three member functions that go together.
        1. destructor.
        2. copy constructor.
        3. assignment operator.
    - If you need to define either of them, you must define all of them. Or, you should not define any of them.
2. **Note:** In C++11, there should be rules of five (a.k.a. **rule of big 5**)
    1. destructor.
    2. copy constructor.
    3. copy assignment operator.
    4. move constructor.
    5. move assignment operator.

## Detailed Information
1. Wrong Sample 
    - lack of assignment operator /copy constructor.
~~~c++
class MyVec{
private:
    int *data;
public:
    // constructor
    MyVec(int n): data(new int[n]){}
    // destructor
    ~MyVec(){delete[] data; };
    // No assignment operator
    // No copy constructor
};
int main(){

    MyVec x(1000);
    MyVec y=x;//Trouble!
    // Both x,y are stack variables.

    return 0;
}
~~~
- Result:
~~~
malloc: *** error for object xxx: pointer being freed was not allocated
~~~
- Shallow Copy:
    - *Default assignment operator* is directly copy value (e.g., address for pointer).
    - y.data = x.data (same address, memory).
- Automatic (stack) variable:
    - While exist scope, call object destructor for each automatic variable (FILO).
    - behavior:
        1. y.destructor()
        2. x.destructor() <-- **runtime-error.**
            - pointer being freed was not allocated

2. Correct sample
~~~c++
class MyVec{
private:
    int *data;
    int size;
public:    
    // constructor
    MyVec(int n): data(new int[n]), size(n){}
    // destructor
    ~MyVec(){delete[] data; };

    // assignment operator (deep copy)
    MyVec& operator=(const MyVec& mv){
        // allocate new space.
        int * newdata = new int[v.size];
        std::copy(v.data, v.data+v.size, newdata);
        
        // release previously allocated space
        delete data;

        data = newdata;
        size = v.size;
        return *this;
    }

    // copy constructor (deep copy)
    MyVec(const MyVec &v):
        data(new int [v.size]),
        size(v.size){
        std::copy(data, data+size, v.data);
    }
};
~~~

## Ref:
[1] [Wiki: Rules of Three](https://en.wikipedia.org/wiki/Rule_of_three_(C%2B%2B_programming))

[2] [The Rule of Three in C++](https://srhuang.github.io/c++/2019/11/11/cplusplus-002.html)

### Date
2022/05/21