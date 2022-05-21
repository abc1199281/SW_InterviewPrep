# What is the RAII (Resource Acquisition is initialization)?

## Summary
- Motivation:
    - Simple and Effective Rule for Resource Management in OOP.  
    - Implicit, and safe.
    - As long as RAII is hold, **if there are no object leaks, there are no resource leaks**.
- Method: 
    - **Holding a resource** is tied to **object lifetime**.
- Notes: 
    - RAII might not coincide with **Scope**. Because *variables allocated on **free store** have lifetimes unrelated to any given scope*. 

## Detailed Information
### Applications
- memory of containers
    - string, vector, map, unordered_map, etc.
- thread, [lock_guard](/4_EfectiveCplusplus/EMC_7_ConcurrencyAPI/ImplementationOf_lock_gurad.md), unique_lock
- ifstream, ofstream
- unique_ptr, shared_ptr

## Ref:
[1] [Wiki: RAII](https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization)

### Date
2022/05/21