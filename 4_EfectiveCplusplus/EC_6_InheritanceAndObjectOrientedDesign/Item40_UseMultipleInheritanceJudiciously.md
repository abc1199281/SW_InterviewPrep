# Item 40: Use multiple inheritance judiciously

### Reference: Item 40

## Summary
1. Multiple inheritance is more complex than single inheritance. 
    - It can lead to new ambiguity issues and to the need for virtual inheritance.
2. Virtual inheritance imposes costs in size, speed, and complexity of initialization and assignment. 
    - It is most practical when virtual base classes have no data.
3. Multiple inheritance does have legitimate uses.
    - One scenario in-volves combining public inheritance from an Interface class with private inheritance from a class that helps with implementation.


## Detailed Information
- Drawback: Enhanced Ambiguity:
    - Although you can still: *mp.BorrowableItem::checkOut();*, not a good design.
    ~~~c++
    class BorrowableItem{
    public:
        void checkOut();
    };
    class ElectronicGadget{
    private:
        bool checkOut() const;
    };
    class MP3Player:
        public BorrowableItem,
        public ElectronGadget
        {/*...*/};
    MP3Player mp;
    mp.checkOut(); // Which one?
    ~~~
- **Deadly MI dimond**:
    - Structure:
        - Base class: File
        - Middle classes (Derived of File): InputFile, OutputFile
        - Bottom class (MI of I/OFile): IOFile
    - Dillema: How many member variable *fileName* should IOFile has?
        1. From code logic, there should be a copy in each path.
        2. From basic logic, each file should only has one name.
    - C++: support both
        1. (Default) copy both.
        2. virtual base class.
        ~~~c++
        class File{};
        class InputFile: virtual public File{/*...*/}
        class OutputFile: virtual public File{/*...*/}
        class IOFile: public InputFile,
                      public OutputFile
        {/*...*/};
        ~~~
    - Real example in C++ STL
        - basic_ios
        - basic_istream, basic_ostream
        - basic_iostream
- Cost of virtual base:
    - Complicated design for compilers.
    - Size of virtual inheritance is larger that of non-virtual.
- Suggestion:
    - Do not use virtual base unless necessary.
    - If necessary, you can avoid putting data in them.
- Another MI case: Person
    - Situation formulation
        - Interface = IPerson
        - Implemented in terms of: PersonInfo
    - Given code:
        - Factory functions
        ~~~c++
        class IPerson{
        public:
            virtual ~IPerson();
            virtual std::string name() const = 0;
            virtual std::string birthDate() const = 0;
        };

        // factory function
        std::shared_ptr<IPerson> makePerson(DatabaseID personIdentifier);

        // function declaration
        DatabaseID askUserForDatabaseID();

        DatabaseID id(askUserForDatabaseID());
        std::shared_ptr<IPerson> pp(makePerson(id));
        ~~~
        - Existing code
        ~~~c++        
        class PersonInfor{
        public:
            explicit PersonInfo(DatabaseID pid);
            virtual ~PersonInfo();
            virtual const char* theName() const;
            virtual const char* theBiethDate() const;
        private:
            virtual const char* valueDelimOpen() const;
            virtual const char* valueDelimClose() const;
        };

        const char* PersonInfo::valueDelimOpen() const{
            return "[";
        }
        const char* PersonInfo::valueDelimClose() const{
            return "]";
        }
        const char* PersonInfo::theName() const{
            static char value[Max_Formatted_Field_Value_Length];
            std::strcpy(value, valueDelimOpen());
            std::strcat(value, valueDelimClose());
            return value;
        }
        ~~~
        - Solution:
        ~~~c++
        class CPerson: public IPerson, private PersonInfo{
        public:
            explicit CPerson(DatabaseID pid):PersonInfo(pid){}
            virtual std::string name() const
            { return PersonInfo::theName();}

            virtual std::string birthDate() const
            { return PersonInfo::theBirthDate(); }

        private: // redefine the inherited delimiter functions
            const char* valueDelimOpen() const { return ""; }
            const char* valueDelimClose() const {return ""; }
        };
        ~~~

### Date
2023/01/02