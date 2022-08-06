# **const** with Functions?

## Summary
-Motivation: Avoid local parameter to be changed
~~~c++
class Dog{
    int age;
    string name;
public:
    Dog() {age = 3; name = "dummy";}

    // const parameters
    //void setAge(int & a){ age = a;a++} // implicitly change a
    void setAge(const int & a){ age = a;a++} // error
    
    /*
    // const here is useless due to passing by value
    void setAge(const int  a){ age = a;a++} 
    */

    // const return value
    const string& getName() {return name;}
    /*
    // const here is useless due to passing by value
    const string getName() {return name;}
    */
    
    // const function
    void pringDogName() const {cout<<name<<endl;}
    // this function will not change any of the variable.
    // void pringDogName() const {cout<<name<<endl;a++;} // error
    // void pringDogName() const {cout<<getName();} // error,
    // can only call other const functions.
    void pringDogName()  {cout<<name<<"non_const"<<endl;} // can be overloaded

};
int main(){
    Dog d;

    // const parameters
    int i = 9;
    d.setAge(i);
    cout << i << endl; // Check whether i==9?

    // const return value
    const string& n = d.getName();
    cout<<n<<endl;

    // const function
    d.printDogName(); // call non-const version pringDogName()

    const Dog d2;
    d2.printDogName(); // call const version pringDogName()

    
}
~~~

## Ref
1. [Advanced C++: const and Functions](https://youtu.be/RC7uE_wl1Uc)

### Date
2022/08/06