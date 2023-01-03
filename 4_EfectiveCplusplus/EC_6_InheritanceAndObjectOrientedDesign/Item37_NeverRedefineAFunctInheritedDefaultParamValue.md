# Item 37: Never redefine a function's inherited default parameter value.

### Reference: Item 37

## Summary
1. Never redefine an inherited default parameter value, because default parameter values are statically bound, while virtual functions - the only functions you should be redefining - are dynamically bound.
    
## Detailed Information
- Simplification:
    - Only virtual functions and non-virtual functions
    - It is always a mistake to redefine a non-virtual functions,
    - so we can safely limit our discussion here to inherting a virtual function with a default parameter value.
- To make it simple:
    - virtual functions--> dynamically bound
    - default parameters are statically bound

### Recap: Dynamic bound and statically bound
- Definition:
    - An object's **static type** is the type you declare it to **have in the program text**.
    - An object's **dynamic type** is determined by the type of the object to which it currently refers. 
- Introduction:
    ~~~c++
    class Shape{
    public: 
        enum ShapeColor {Red, Green, Blue};
        virtual void draw(ShapeColor color = Red) const = 0;
    };
    class Rect: public Shape{
    public:
        // Note: assign different default params are really bad!!!
        virtual void draw(ShapeColor color = Green) const = 0;
    };
    class Circle: public Shape{
        virtual viod draw(ShapeColor color) const; 
        // Note: force client to assign parameter
        // Static bound: not inherit the default param value
        // Dynamic bound (pointer/reference): get param value from base class.
    };

    Shape* ps;              // Static type = Shape*, Dynamic type = null
    Shape* pc = new Circle; // Static type = Shape*, Dynamic type = Circle*
    Shape* pr = new Rect;   // Static type = Shape*, Dynamic type = Rect*

    pc->draw(Shape::Red);   // Circle::draw(Shape::Red)
    pr->draw(Shape::Red);   // Rect::draw(Shape::Red)

    // Contradiction
    pr->draw(); 
    // Rect::draw(Shape::Red)-->default params (satatic bound) from base class
    ~~~
    - Please 

- What if we follow the rule: Code duplication -> dependencies.
    - Problem:
    ~~~c++
    class B{
        virtual void draw(ShapeColor color=Red) const = 0;
    };
    class D{
        virtual void draw(ShapeColor color=Red) const ;
        // Code duplication = dependencies.
    };
    ~~~
    - Solution, Alternative: Item 35., non-virtual interface (NIV)
    ~~~c++
    class Shape{
    public:
        enum ShapeColor {Red, Green, Blue};
        // virtual to non-virtual, cannot be redefine
        void draw(ShapeColor color = Red) const
        { doDraw(color); }
    private:
        virtual void doDraw(ShapeColor = color) const = 0;
    };
    class Rect{
    private:
        // No need to assign the default params.
        void doDraw(ShapeColor = color) const; 
    };
    ~~~

### Date
2023/01/01