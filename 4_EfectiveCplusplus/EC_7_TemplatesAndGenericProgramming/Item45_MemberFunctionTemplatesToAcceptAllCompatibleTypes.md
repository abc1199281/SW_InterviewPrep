# Item 45: Use member functions template to accept all compatible types

### Reference: Item 45

## Summary
- Motivation: How do smart pointers, like the real pointers, support implicit conversions.
- Use member function templates to generate functions that accept all compatible types.
- If you declare member templates for generalized copy construction or generalized assignment, you'll still need to declare the normal copy constructor and copy assignment operator, too.

## Detailed Information
1. Problem Formulation
    - How do smart pointers, like the real pointers, support implicit conversions.
    ~~~c++
    class Top{/*...*/};
    class Middle:public Top{/*...*/};
    class Bottom:public Middle{/*...*/};
    Top *pt1 = new Middle;  // convert Middle*-->Top*
    Top *pt2 = new Bottom;  // convert Bottom*-->Top*
    const Top *pct2 = pt1;  // convert Top* --> const Top*
    ~~~
    - In smart ptr, we hope the following code works
    ~~~c++
    template<typename T>
    class SmartPtr{
    public:
        explicit SmartPtr(T *realPtr);
        //...
    };
    // convert SmartPtr<Middle> --> SmartPtr<Top>
    SmartPtr<Top> pt1 = SmartPtr<Middle>(new Middle);
    // convert SmartPtr<Bottom> --> SmartPtr<Top>
    SmartPtr<Top> pt2 = SmartPtr<Bottom>(new Bottom);
    // convert SmartPtr<Top> --> SmartPtr<const Top>
    SmartPtr<const Top> pct2 = pt1;
    ~~~
    - Why it fails?
        - There is no inherent relationship among different instantiations of the same template.
        - To make it work, we have to program them explicitly.

2. Solution
    - Observations;
        - To cope with further inheritance, we need a ctor templates.
        - Name: **member templates**
        ~~~c++
        template<typename T>
        class SmartPtr{
        public:
            template<typename U> // generalized constructor
            SmartPtr(const SmartPtr<U>& other);
        };
        ~~~        
    - Constraint: follow inhertance
        - Method: utilize real pointers        
        ~~~c++
        template<typename T>
        class SmartPtr{
        public:
            template<typename U>
            SmartPtr(const SmartPtr<U>&other) // initialize this held ptr.
            :heldPtr(other.get()){/*...*/}    // with other's held ptr
            T* get() const {return heldPtr;}
            //...
        private:            // built-in pointer held
            T* heldPtr;     // by the SmartPtr
        };
        ~~~
3. Example: share_ptr
    ~~~c++
    template<class T>
    class shared_ptr{
    public:

        // normal ctor.
        shared_ptr(shared_ptr const& r); 

        // ctor from any compatible build-in pointer.
        template<class Y>
            explicit shared_ptr(Y* p);

        template<class Y>
            explicit shared_ptr(weak_ptr<Y> const& r);

        // no const due to Item 13., auto_ptr modified content while copy.
        template<class Y>
            explicit shared_ptr(auto_ptr<Y>& r); 

        // generalized copy ctor.
        // no explicit=support implicit conversion.
        template<class Y>
            shared_ptr(shared_ptr<Y> const& r); 

        // normal assignment 
        shared_ptr& operator=(shared_ptr const& r);

        // assignment from any compatible shared_ptr or 
        template<class Y>
            shared_ptr& operator=(shared_ptr<Y> const& r); 

        // auto_ptr
        template<class Y>
            shared_ptr& operator=(auto_ptr<Y>& r);
    };
    ~~~

### Date
2022/12/27