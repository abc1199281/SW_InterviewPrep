# A simple, minimal, example of C++ Expression Templates 

### Ref: [A simple, minimal, example of C++ Expression Templates](https://bnikolic.co.uk/blog/cpp-expression-minimal)

## Summary
0. Motivation: 
    - Original: 4 temperary matrix are created.
    - Expression templates: eliminate temperary matrix.
        - Less memory, dramatically  enhance speed.
    ~~~c++
    BigMatrix result = m1*m2*m3*m4*m5;
    ~~~

## Detailed information
- The idea here is to illustrate addition of vectors (in this case I'm using plain old std::vector). The expression template mechanism below is in fact so simple here that it only supports the addition operation and there are several shortcomings compared to a proper (and much longer) implementation. However it shows three clear advantages that are critical in high-performance code:

    1. No creation of temporaries of length order N (where N is the number of elements)
    2. Only a single iteration need be made through all of the vectors being added
    3. If only a subset of elements of the result is requested, then only these elements are computed

- Note: refer to Bojan Nikolic <bojan@bnikolic.co.uk>
~~~c++
#include <vector>
#include <iostream>

/// For comparison, this is an addition operator on standard
/// std::vectors the old-fashioned way
template<class T>
std::vector<T> operator+(const std::vector<T>&a, 
                         const std::vector<T>&b)
{
    std::vector<T> res(a.size());
    for(size_t i = 0;i<a.size();++i)
        res[i]=a[i]+b[i];
    return res;
}

// This is trait class for ops which actually just represent the value
// of a single argument
struct valueop{};
// This is for the addition operation
struct addop{};

template<class E1 = std::vector<double>, 
         class E2 = std::vector<double>,
         class op = valueop>
struct binop
{
    const E1 & left;
    const E2 & right;
    binop(const E1& left,
          const E2& right,
          op opval):
          left(left),
          right(right)
          {};
    // Construction with just one value and default operator is taken
    // to mean that this is a "terminal" value
    binop(const E1 & val);
};

template<>
binop<std::vector<double>,
      std::vector<double>,
      valueop>
      ::binop(const std::vector<double> &val):left(val), right(val){}

/// Evaluete the i-th element of an expression
template<class E1, class E2, class op>
double eval(const binop<E1, E2, op> &o, size_t i)
{
    // Default implementation returns 0 as that is identity for 
    // addition/substraction
    return 0;
}

/// Evaluation of a "valueop" just returns the value
template<class T>
double eval(const binop<T, T, valueop> &o,
            size_t i)
{
    return o.left[i];
};

/// Evaluation of "addop" adds the corresponding elements
template<class E1, class E2>
double eval(const binop<E1, E2, addop> &o, size_t i)
{
    return eval(o.left, i) + eval(o.right, i);    
};

template<class E1, class E2>
binop<E1, E2, addop> operator+(const E1 &left,
                               const E2 &right)
{
    return binop<E1, E2, addop>(left, right, addop());
}

template<class T>
binop<T, T, valueop> mkVal(T& val)
{
    return binop<T, T, valueop>(val);
}

int main()
{
    std::vector<double> a(10, 1.0), b(10, 2.0);

    // Addition the old way, entire vector is computed.
    std::cout<<((a+b+a+b)[3])<<std::endl;

    // Now do it the expression template way
    binop<> ba(a), bb(b);
    // If you've got C++ 0x features then you can do:
    // auto bc=mkVal(a);

    // Print 3rd element of the sum, only the sum for the third element
    // is computed.
    std::cout<<eval(ba+bb+ba+bb, 3)<<std::endl;
}
// -Xclang -ast-print -fsyntax-only
~~~

### Date
2022/12/28