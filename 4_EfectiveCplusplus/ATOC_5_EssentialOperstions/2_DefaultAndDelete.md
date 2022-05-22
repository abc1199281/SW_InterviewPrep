# What is the usage of =default and =delete?
## Summary
- =default : use default constructor
- =delete : forbidden a operation.

## Sample
- =default
~~~c++
class Y{
public:
    // I really want to use default copy constructor.
    Y(const Y&) =default; 
    // I really want to use default move constructor.
    Y(Y&&) = default; 
};
~~~
- =delete
~~~c++
class Shape(){
public:
    Shape(const Shape&) = delete; // no copy operation
}
~~~

### Date
2022/05/22