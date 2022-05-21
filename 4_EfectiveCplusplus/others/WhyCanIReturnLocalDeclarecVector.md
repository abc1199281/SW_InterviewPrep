# Why Can I return a local declared vector?
## Questions
- Undefined behavior
~~~c++
class MyVec(){
private:

};
return_local_variable(){

}

~~~
- OK behavior (commonly seen)

## Simple answer
