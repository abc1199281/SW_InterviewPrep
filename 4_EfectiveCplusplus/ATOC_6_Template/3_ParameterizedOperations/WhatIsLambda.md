# What is the Lambda expression?

### Reference: 6.1 Introduction Template. 

## Summary
0. Definition:
    - a shorthand notation for a function object.
1. Sample:
    ~~~c++
    void f(const Vector<int>&vec, const list<string>& lst, int x, const string&s){
        cout<<"number of values less than "<<x<<":"<<
            count(vec,[&](int a){return a<x;})<<endl;
    }
    ~~~

## Detailed Information
0. Behavior:
    - generate the same function object as Less_than<int>{x}
    - [&]: capture list
        - &: reference
        - =x: copy 
        - []: no capture new item.
1. Another sample: for_all
    ~~~c++
    template<typename C, typename Oper>
    void for_all(C& c, Oper op)
    // requires Sequence<C> && Callable<Oper, Value_type<C>>
    {
        for(auto &x: c)
            op(x);
    }
    // usage
    vector<unique_ptr<Shape>> v;
    while(cin)
        v.push_back(read_shape(cin));
    // draw_all()
    for_all(v,[](unique_ptr<Shape>& ps){ps->draw();})
    // rotate_all()
    for_all(v,[](unique_ptr<Shape>& ps){ps->rotate(45);})
    ~~~
2. Better initialization
    - Before
    ~~~c++
    enum claass init_mode{zero, seq, cpy, patrn};
    vector<int> v;
    switch(m){
        case zero:
            //...
            break;
        case cpy:
            //...
            break;
        // might miss a case.
    }
    //... // might confusing.
    if(m==seq)
        v.assign(p,q);// Might cause error.
    ~~~
    - After: Initialization via lambda expression.
    ~~~c++
    vector<int> v = [&]{ // Force initialization
        switch(m){
        case zero:
            return vector<int>(n);
        case seq:
            return vector<int>{p,q};
        case cpy:
            return arg;
        }
    }();
    ~~~

3. Parameterized Operations
    - Function template
    - Function object: 
        - an object that can carry data and be called like a function
    - **Labda expression**
        - a shorthand notation for a function object.

### Date
2022/06/11