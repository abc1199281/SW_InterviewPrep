# Item 43: Know how to access names in templatized base class

### Reference: Item 43

## Summary
1. In derived class template, refer to names in base class templates via 
    1. "this->" prefix,
    2. using declarations,
    3. or an explicit base class qualification (not recommend)
2. In some sense, when we cross from Object-Oriented C++ to Template C++, inheritance stops working (Item 1).

## Detailed Information
1. Problem formulation
    - Scenario:
        - write an application that can send messages to several companies.
        - messages can be sent in either encripted or clear text. (tempalte-class)
        - Add a logger (derived class)    
    - Note:
        - To side-step the issue of hiding inherited names (Item 33) and redefining an inherited non-virtual function (Item 36), *sendClearMsg* is different from *sendClear*.

    ~~~c++
    class CompanyA{
        void sendCleartext(const std::string& msg);
        void sendEncryptedtext(const std::string& msg);
    }
    class CompanyB{
        void sendCleartext(const std::string& msg);
        void sendEncryptedtext(const std::string& msg);
    }
    class MsgInfo{/*...*/};

    // The applicaion: Template-based solution
    template<typename Company>
    class MsgSender{
    public: 
        void sendClear(const MsgInfo& info){
            std::string msg;
            // generate info based MsgInfo.
            Company c;
            c.sendCleartext(msg);
        }
        void sendEncrypted(const MsgInfo& info){
            /*...like wise...*/
        }
    }

    // Derived class: Add logger
    template<typename Company>
    class LoggingMsgSender: public MsgSender<Company>{
    public:
        void sendClearMsg(const MsgInfo& info){
            // write log
            sendClear(info); // error
            // write log 
        }
    }
    ~~~
    - Reason:
        - When encounter *class LoggingMsgSender*, compilers don't know the class it inherited its from.
        - Compiler regects the inhertanced member function, because it knows interface of base template is not guaranteed. That is to say, "total template specialization" can break the general rule of MsgSender.

2. Sol 1: this->
~~~c++    
    template<typename Company>
    class LoggingMsgSender: public MsgSender<Company>{
    public:
        void sendClearMsg(const MsgInfo& info){
            // write log
            this->sendClear(info); // this->
            // write log 
        }
    }
~~~
3. Sol 2: using declaration
    - This is different from Item 33,
        - where base class names are hidden by derived class name.
    - In Item 43,
        - compilers don't search base class scopes unless we tell them to.
~~~c++    
    template<typename Company>
    class LoggingMsgSender: public MsgSender<Company>{
    public:

        // Tell the compiler to assume that sendClear is in the base class.
        using MsgSender<Company>::sendClear; 
        
        void sendClearMsg(const MsgInfo& info){
            // write log
            sendClear(info);
            // write log 
        }
    }
~~~
4. Sol 3: explicit qualification (not recommended)
    - fails at virtual functions and turns of the virtual binding behavior.
    
~~~c++    
    template<typename Company>
    class LoggingMsgSender: public MsgSender<Company>{
    public:        
        void sendClearMsg(const MsgInfo& info){
            // write log

            // Assumes that sendClear will be inherited.
            MsgSender<Company>::sendClear(info); 
            // write log 
        }
    }
~~~
5. Example of total template specialization treat
    - Because of this syntax, interface of base template is not guaranteed.    
~~~c++
class CompanyZ{
    void sengEncrypted(const std:;string& msg); // Don't support sendCleartext
}

// Total template specialization
// neigher template nor class, only for CompanyZ
template<>  
class MsgSender<CompanyZ>{
    void sendSecret(const MsgInfo& info){/*...*/}
}
~~~

### Date
2022/12/25