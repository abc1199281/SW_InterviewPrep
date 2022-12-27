# Item 44: Factor Parameter-independent Code out of templates.

### Reference: Item 44

## Summary
- Templates generate multiple classes and multiple functions, so any template code not dependent on a template parameter causes bloat.
- Bloat due to non-type template parameters can often be eliminated by replacing template parameters with functions parameters or class data members.
- Bloat due to type parameters can be reduced by sharing implementations for instantiation types with identical binary representations.

## Detailed Information
1. Problem formulation
    - Motivation of templates:
        - Utilizing independence of type, templates serve as a wonderful way to save teim and avoid code replication.
        - You let compilers instantiate specific classes only when needed.
        - You write one template and let the compilers do the rest.
    - Problem:
        - **Code bloat**: binaries with replicated code, or data.
        - Although source code look fit and trim, object can be fat and flabby.
        - Tool: **Commonality and variability anaylsis**
    - A case of template induced code bloat
    ~~~c++
    template<typename T,    // template for nxn matrices of objects of type T; 
             std::size_t n> // non-type parameter
    class SquareMatrix{
    public:
        void invert();
    };  
    SquareMatrix<double, 5> sm1; sm1.invert();
    SquareMatrix<double, 10> sm1; sm1.invert();
    ~~~
2. Solution 1: **Commonality and variability anaylsis**
    - When some part of the functions are essential the same.
        - factor the common code out of the two functions, put it into a third function.
    - In non-templates, you can see the duplication; whereas, in template code, replication is implicit. We have to train ourself to sense the replication.
    - Instinct solution
    ~~~c++
    template<typename T>        // size-independent base class for
    class SquareMatrixBase{     // square matrices
    protected:
        void invert(std::size_t matrixSize); // invert amtrix of the given size
    };
    template<typename T, std::size_t n>
    class SquareMatrix: private SquareMatrixBase<T>{
    private:
        using SquareMatrixBase<T>::invert;// Item 43 and 33.
    public:
        void invert(){invert(n);} // make inline call to base class version.
    };
    ~~~
    - Problem: How does SquareMatrixBase::invert know what data to operate on?
        - How to pass data type from inherited class
3. Solution 2:
    - Candidate: add another parameter to SquareMatrixBase::invert()
        - invert is usually not the only one who need type info functions.
        - If there are other functions, pass memory to base class.
    - Have SquareMatrixBase store a pointer to the memory
    ~~~c++
    template<typename T>
    class SquareMatrixBase{
    protected:
        SquareMatrixBase(std::size_t n, T* pMem)    // store matrix size and a 
        : size(n), pData(pMem){}                    // ptr to matrix values
        void setDataPtr(T *ptr){pData = ptr;}       // reassign pData
    private:
        std::size_t size;                           // size of matrix
        T *pData;                                   // pointer to matrix values
    };
    template<typename T, std::size_t n>
    class SquareMatrix: private SquareMatrixBase<T>{
    public:
        SquareMatrix()                      // send matrix size and
        : SquareMatrixBase<T>(n, data){}    // data ptr to base class
    private:
        T data[n*n]; // Note here the n is compile-time constant.
    };
    ~~~
    - Objects of such types have no need for dynamic memory allocation, but the objects themselves could be very large. Alternatively, put on the heap.
    ~~~c++
    template<typename T, std::size_t n>
    class SquareMatrix: private SquareMatrixBase<T>{
    public:
        SquareMatrix()                  // set base class data ptr to null
        :SquareMatrixBase<T>(n,0),      // allocate memory for matrix 
         pData(new T[n*n])              // values, save a ptr to the
        {this->setDataPtr(pData.get());}// memory, and give a copy of it
                                        // to the base class        
    private:
        boost::scoped_array<T> pData; // see Item 13 for info on 
                                      // boost::scoped_array
    };
    ~~~

### Date
2022/12/27