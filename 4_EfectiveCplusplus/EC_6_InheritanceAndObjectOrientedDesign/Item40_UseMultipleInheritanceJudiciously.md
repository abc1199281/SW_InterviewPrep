# Item 38: Model "has-a" or "is-implemented-in-terms-of" through composition

### Reference: Item 38

## Summary
1. **Composition** has meanings completely different from that of public inheritance.
2. In the **application domain**, composition means **has-a**. 
3. In the **implementation domain**, it means **is-implemented-in-terms-of**

- 2 Domains:
    - **Application domain**:
        - Objects correspond to things in the world you are modeling
        - E.g., people, vehicles, video, etc.
        - Composition = **has-a**
    - **Implementation domain**:
        - Objects are purely implementation artifacts.
        - e.g., buffers, mutexes, search trees, etc.
        - Composition = **is-implemented-in-terms-of**

## Detailed Information
- Composition
    - The relationship between types that arises when objects of one type **contain** objects of another type.
    - Synonyms:
        - *layering, containment, aggregation, embedding*
    ~~~c++
    class Address{/*...*/};
    class PhoneNumber{/*...*/};
    class Person{
    public:
        /*...*/
    private:
        std::string name;           // Composed object.
        Address address;            // ditto
        PhoneNumber voiceNumber;    // ditto
        PhoneNumber faxNumber;      // ditto
    };
    ~~~
- 2 Domains:
    - **Application domain**:
        - Objects correspond to things in the world you are modeling
        - E.g., people, vehicles, video, etc.
        - Composition = **has-a**
    - **Implementation domain**:
        - Objects are purely implementation artifacts.
        - e.g., buffers, mutexes, search trees, etc.
        - Composition = **is-implemented-in-terms-of**
- Example of Implementation domain
    - Target: **Set** with optimal space complexity
        - **std::set** require
            - Space: Three pointers for balanced search trees.
            - Time: O(logn)
        - Alternative: implementated in terms of a **std::list**.
    - Error:
        - Set is *not* a list, so public inheritance doesn't work.
        ~~~c++
        template<typename T>
        class Set: public std::list<T>{/*...*/};
        ~~~
    - Good:
        - Set is implemented in terms of list
        ~~~c++
        template<class T>
        class Set{
        public:
            bool member(const T& item) const;
            void insert(const T& item);
            void remove(const T& item);
            std::size_t size() const;
        private:
            std::list<T> rep; // Is implemented in terms of list
        };
        ~~~
### Set implementation
~~~c++
template<typename T>
bool Set<T>::member(const T&item) const{
    return std::find(rep.begin(), rep.end(), item) != rep.end();
}

template<typename T>
void Set<T>::insert(const T& item){
    if(!member(item)) rep.push_back(item);
}

template<typename T>
void Set<T>::remove(const T&item){
    typename std::list<T>::iterator it = 
        std::find(rep.begin(), rep.end(), item);
    if(it!= rep.end()) rep.erase(it);
}

template<typename T>
std::size_t Set<T>::size() const{
    return rep.size();
}
~~~   

### Date
2023/01/01