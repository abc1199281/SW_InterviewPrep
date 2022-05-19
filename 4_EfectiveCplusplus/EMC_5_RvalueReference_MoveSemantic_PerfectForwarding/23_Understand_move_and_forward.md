# Item 23: understand std::move & std::forward

### Note:
- All **parameters** are lvalue.
~~~c++
void f(widget&& w);
// w is parameters, lvalue with rvalue reference type.
~~~

## Quick answer
1. **std::move**:
    - std::move forcely transfers parameter into rvalue.
2. **std::forward**    
    - When argument is rvalue, std::forward transfers argument into rvalue.
3. Both of them don't do anything except tranforming type.

~~~c++
template<typename T>
typename remove_reference<T>::type&& move(T&& param)
{
    using ReturnType = typename remove_reference<T>::type&&;
    return static_cast<ReturnType>(param);
}
~~~

