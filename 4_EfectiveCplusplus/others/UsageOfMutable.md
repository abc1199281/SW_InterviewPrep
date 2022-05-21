# What is the usage of mutable?

## Quick answer
- The keyword mutable is mainly used to allow a particular data member of const object to be modified. 
- This task can be easily performed by using the *mutable* keyword. 
~~~c++
class Text{
public:
    int x;

    // defining mutable variable y
    // now this can be modified.
    mutable int y;

    Test():x(4),y(10){}
};
int main(){
    // t1 is set to constant.
    const Test t1;

    // trying to change the value.
    t1.y = 20; // Work.

    // Error
    t1.x = 8;    
}
~~~

## Simple answer
### Ref
1. [Storage Classes with examples](https://www.geeksforgeeks.org/storage-classes-in-c-with-examples/)