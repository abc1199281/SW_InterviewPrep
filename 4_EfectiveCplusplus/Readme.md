# Rules of Three
## Motivation
*Do things right and do the rignt thing.*

There are plenty ways to implement things. But, how to do things right? 

1. We should follow the new standard C++ so that we can utilize more effective tools.
2. We should understand the foundamental of C/C++ scheme (e.g., memory allocation).

## Category Method
Here I record all the questions come into my mind while learning C++11/C. There are several levels for me to record.

- [Basic] :
    - Classic C++/C concepts.
    - Entry level C++11 concept: 
        - Why this new function?
        - Difference

- [Middle] :
    - Important concepts.
    - Eaisly confused concepts.
    - Foundamental implementation of C++11.

- [Advanced] :
    - Integration with several concepts.
    - Newer than C++11


## Structure of each answer.
### Summary
- just high level / quick answer
### Detailed information (if applicable)
- e.g., What's the method to implement this scheme?

# Outline
### Basic
- [[EC_3_ResourceManage] What is the RAII? [2022/05/21]](EC_3_ResourceManagement/RAII.md)
- [[EMC_5_MoveSemanticForward] 23: understand std::move & std::forward [2022/05/19]](EMC_5_RvalueReference_MoveSemantic_PerfectForwarding/23_Understand_move_and_forward.md)
- [[EMC_8_Tweaks] 42. What is the difference between .push_back() and .emplace_back()? [2022/05/18]](EMC_8_Tweaks/Diff_emplace_back_push_back.md)
- [[others] What is the lvalue and rvalue? [2022/05/19]](others/left_value_right_value.md)
- [[others] What is the difference between Malloc & New? (free & delete) [2022/05/18] ](others/Diff_New_Malloc.md)
- [[others] What is the difference between function argument and parameter? [2022/05/19]](others/Diff_function_argument_parameter.md)

- [[others] What is the Uniform Initialization? [2022/05/20]](others/UniformInitialization.md)
- [[others] What is the Rules of Three (or Rules of Big 5) in C++? [2022/05/21]](EC_2_ConstructorDestructorsAndAssignmentOperators/RulesOfThree.md)

- [[others] What is the usage of mutable? [2022/05/21]](others/UsageOfMutable.md)
- [[others] What is the automatic variable? [2022/05/21]](others/WhatIsAutomaticVariable.md)

### Middle
- [[EMC_7_Concurrency] What is the implementation of lock_guard? [2022/05/21]](EMC_7_ConcurrencyAPI/ImplementationOf_lock_gurad.md)
- [[others] What is the initial value of int array? [2022/05/21]](others/InitialValueOfArray.md)
- [[others] What is the Memory layout? [2022/05/21]](others/MemoryLayout.md)
- [[others] What is the Storage Classes? [2022/05/21]](others/StorageClasses.md)

### Advanced
- [[others] Why can I return a local declared vector? [2022/05/21]](others/WhyCanIReturnLocalDeclarecVector.md)

## Reference
[1] Effective C++: 55 Specific Ways to Improve Your Programs and Designs 3rd Edition, Scott Meyers.

[2] Effective Modern C++: 42 Specific Ways to Improve Your Use of C++11 and C++14 1st Edition, Scott Meyers.

[3] A Tour of C++, Bjarne Stroustrup