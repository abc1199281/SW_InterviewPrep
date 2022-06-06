# What is the Structured binding?

###  Reference: 3.6.3: Structured binding

## Summary
1. Motivation:    
    - Usually, a function return a value.
    - Structured binding allows us to effeciently return many values.
    - Application:
        - map in for loop
2. Sample
    ~~~c++
    map<string, int> m;

    // [key, value] is a kind of structured binding.
    for(const auto [key, value]: m)
        cout<<"{"<< key<<","<<value<<"}"<<endl;
    ~~~
   
## Detailed information
1. Another sample
~~~c++
struct Entry{
    string name;
    int value;
};

Entry read_entry(istream&is){
    string s;
    int i;
    is>>s>>i;
    return {s,i}; // return a struct.
}

// conventional method
auto e = read_entry(cin);
cout<<"{"<< e.name<<","<<e.value<<"}"<<endl;

// structured bindind.
auto [name, value] = read_entry(cin);
cout<<"{"<< name<<","<< value<<"}"<<endl;
~~~

### Date
2022/06/06