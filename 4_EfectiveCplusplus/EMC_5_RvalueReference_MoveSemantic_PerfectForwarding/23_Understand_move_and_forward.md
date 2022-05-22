# Item 23: understand std::move & std::forward

## Summary
1. **std::move**:
    - std::move forcely transfers parameter into rvalue.
2. **std::forward**    
    - When argument is initialized with rvalue, std::forward transfers argument into rvalue.
3. Both of them don't do anything except tranforming type.

~~~c++
template<typename T>
typename remove_reference<T>::type&& move(T&& param)
{
    using ReturnType = typename remove_reference<T>::type&&;
    return static_cast<ReturnType>(param);
}
~~~
## Example

~~~c++
#include <cstdio>
class Widget{
    public:
        Widget(){}
        Widget(const Widget&){
            puts("copy ctor");
        }
        Widget(Widget&&){
            puts("move ctor");
        }
}

Widget make_W() {
    Widget w; 
    return w;
}
int main(){
    Widget w1;
    Widget w2(make_W);
}
~~~

### Note:
- All **parameters** are lvalue.
~~~c++
void f(widget&& w);
// w is parameters, lvalue with rvalue reference type.
~~~
### Date
2022/05/21