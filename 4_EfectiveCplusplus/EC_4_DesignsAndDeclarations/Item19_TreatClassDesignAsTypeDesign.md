# Item 19: Treat Class Design as Type design

### Reference: Item 19

## Summary
- Class design is type design. Before defining a new type, be sure to consider all the issues discussed in the Item.

## Detailed Information
- How should objects of your new type be created and destroyed?
    - design of ctor/dtor, memory allocation/deallocation
    - Item 49-52
- How should object initialization differ from object assignment?
    - Item 4
- What does it mean for objects of your new type to be passed by value?
    - ctor
- What are the restrictions on legal values for your new type?
    - Invariants
- Does your new type fit into an inheritance graph?
    - Item 7, 34, 36
- What kind of type conversions are allowed for your new type?
    - Item 15
- What operators and functions make sense for the new type?
    - Item 23, 24, and 46
- What standard functions should be disallowed?
    - Item 6
- Who should have access to the members of your new type?
- What is the "undeclared interface" of your new type?
    - Item 29
- How general is your new type?
    - Consider class template
- Is a new type really what you need?

### Date
2023/01/04