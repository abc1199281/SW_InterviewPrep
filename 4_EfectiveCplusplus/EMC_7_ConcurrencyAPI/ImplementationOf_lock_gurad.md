# What is the implementation of lock_guard?

### Prerequist
- [[EC_3_ResourceManage] What is the RAII?](EC_3_ResourceManagement/RAII.md)


## Simple answer
- Motivation:
    - The class lock_guard is a mutex wrapper that provides a convenient **RAII-style** mechanism for owning a mutex for the duration of a scoped block.
    
- Method: 
    - Using **RAII** and **stack-unwinding** to achieve **exception-safe** while using a mutex for a block.

## Detailed Information
### Implementation
~~~c++
template <class Mutex> class lock_guard {
private:
    Mutex& mutex_;

public:
    // Constructor
    lock_guard(Mutex& mutex) : mutex_(mutex) {  
        mutex_.lock(); 
    }

    // Destructor
    ~lock_guard() { 
        mutex_.unlock(); 
    }
    
    lock_guard(lock_guard const&) = delete;
    lock_guard& operator=(lock_guard const&) = delete;
};
~~~

### Usage of lock_guard
- lock_guard is exception-safe based on **stack-unwinding** and **RAII** scheme.

~~~c++
extern void unsafe_code(); // could throw exception.

using std::mutex;
using std::lock_guard;

mutex g_mutex;

void access_critical_section()
{
    lock_guard<mutex> lock(g_mutex);
    // call constructor of lock_guard.
    // In the constructor, g_mutex.lock()

    unsafe_code();

    // call lock.destructor while existing this scope.
    // during the destruction, g_mutex.unlock()
    // Why is it exception-safe?
    // Even an exception is throwed, stack-unwinding scheme will also call the destructor of lock_guard.
    // Then, g_mutex.unlock() is also called.
}
~~~


## Ref:

[1] [Wiki: RAII (Chinese)](https://zh.wikipedia.org/wiki/RAII)

[2] [lock_guard, cppreference.com](https://en.cppreference.com/w/cpp/thread/lock_guard)

### Date
2022/05/21