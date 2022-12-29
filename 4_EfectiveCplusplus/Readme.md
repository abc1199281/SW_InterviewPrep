# Effective C++
## Motivation
*Do things right and do the rignt thing.*

There are plenty ways to implement things. But, how to do things right? 

1. We should follow the new standard C++ so that we can utilize more effective tools.
2. We should understand the foundamental of C/C++ scheme (e.g., memory allocation).

So, there are three classic books I read, and I'll catogarize the concepts based on them.

1. (EC) Effective C++: 55 Specific Ways to Improve Your Programs and Designs 3rd Edition, Scott Meyers. 
2. (EMC) Effective Modern C++: 42 Specific Ways to Improve Your Use of C++11 and C++14 1st Edition, Scott Meyers.
    - Detailed concept while using C++11
3. (ATOC2) A Tour of C++ (2e), Bjarne Stroustr
    - Relative entry lecel description for C++11 / C++

## Category Method
Here I record all the questions come into my mind while learning C++11/C. There are several levels for me to record.

- [Basic] :
    - Classic C++/C concepts.
    - Entry level C++11 concept: 

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
- [[ATOC_1_6] What is the difference between **const** and **constexpr**?](/4_EfectiveCplusplus/ATOC_1_Basics/6_ConstConstexpr.md)
- [[ATOC_3_5] What is the Exception?](/4_EfectiveCplusplus/ATOC_3_Modularity/5_1_Exceptions.md)
- [[ATOC_3_5] What is the Class Invariant?](/4_EfectiveCplusplus/ATOC_3_Modularity/5_2_ClassInvariant.md)
- [[ATOC_3_5] What is the Static assertions?](/4_EfectiveCplusplus/ATOC_3_Modularity/5_3_StaticAssertions.md)
- [[ATOC_3_6] What is the Structured bindind?](/4_EfectiveCplusplus/ATOC_3_Modularity/6_3_StructuredBinding.md)
- [[ATOC_4_2] What is the Uniform Initialization?](/4_EfectiveCplusplus/ATOC_4_Classes/2_3_UniformInitialization.md)
- [[ATOC_5_1] What is the Rules of Three (or Rules of Big 5, the rule of zero) in C++?](/4_EfectiveCplusplus/ATOC_5_EssentialOperstions/1_RulesOfThree.md)
- [[ATOC_5_2] What is the =default and =delete specifier?](/4_EfectiveCplusplus/ATOC_5_EssentialOperstions/2_DefaultAndDelete.md)
- [[ATOC_5_3] What is the RAII?](/4_EfectiveCplusplus/ATOC_5_EssentialOperstions/3_RAII.md)
- [[ATOC_6_2] What is the *template*?](/4_EfectiveCplusplus/ATOC_6_Template/2_ParameterizedTypes/WhatIsTemplate.md)

- [[EMC_8_Tweaks] 42. What is the difference between .push_back() and .emplace_back()?](EMC_8_Tweaks/Diff_emplace_back_push_back.md)
- [[others] What is the Polymorphism?](/4_EfectiveCplusplus/others/Polymorphism.md)
- [[others] What is the lvalue and rvalue?](others/left_value_right_value.md)
- [[others] Difference between Malloc & New? (free & delete)](others/Diff_New_Malloc.md)
- [[others] Difference between function argument and parameter?](others/Diff_function_argument_parameter.md)

- [[others] What is the usage of mutable?](others/UsageOfMutable.md)
- [[others] Automatic variable?](others/WhatIsAutomaticVariable.md)
- [[others] Can I initialize array with variable specified by *const*?](/4_EfectiveCplusplus/others/CanI_InitializeArrayWithVariable.md)

### Middle
- [[EMC_7_Concurrency] Implementation of lock_guard](EMC_7_ConcurrencyAPI/ImplementationOf_lock_gurad.md)
- [[EC_5_Implementations] What is the stack unwinding?](/4_EfectiveCplusplus/EC_5_Implementations/WhatIsStackUnwinding.md)
- [[others] What is the initial value of int array?](others/InitialValueOfArray.md)
#### - OOP
- [[ATOC_4_4] Virtual Table (v-table)](/4_EfectiveCplusplus/ATOC_4_Classes/4_VirtualTable.md)
- [[ATOC_4_4] What is the difference between non-virtual, virtual, and pure virtual functions](/4_EfectiveCplusplus/ATOC_4_Classes/4_VirtualFunctionsVSPureVirtualFunctions.md)
- [[EC_6_Inheritance] 32, public inheritance follows models "is-as," i.e., Liskov Substitution Principle.](/4_EfectiveCplusplus/EC_6_InheritanceAndObjectOrientedDesign/Item32_MakeSurePublicInheritanceModelsIsAs.md)

#### - Memory
- [[others] What is the Memory layout?](others/MemoryLayout.md)
- [[others] What is the Storage Classes?](others/StorageClasses.md)

#### - Move semantic
- [[EMC_5_MoveSemanticForward] 23: understand std::move & std::forward](EMC_5_RvalueReference_MoveSemantic_PerfectForwarding/23_Understand_move_and_forward.md)
- [[others] [Classic] Motivation for Move semantics and rvalue references in C++11](others/Blog_MoveSemanticsAndRValueReferences.md.md)

#### - Templates
- [[ATOC_6_2] Constrained Template arguments](/4_EfectiveCplusplus/ATOC_6_Template/2_ParameterizedTypes/1_WhatIsConstrainedTemplate.md)
- [[ATOC_6_2] Non-type template arguments / value arguement](/4_EfectiveCplusplus/ATOC_6_Template/2_ParameterizedTypes/2_WhatIsNonTypeTemplate.md)
- [[ATOC_6_2] Template arguments deduction](/4_EfectiveCplusplus/ATOC_6_Template/2_ParameterizedTypes/3_WhatIsTemplateArgumentDeduction.md)
- [[ATOC_6_4] Variable Template](/4_EfectiveCplusplus/ATOC_6_Template/4_TemplateMechanisms/WhatIsVariableTemplate.md)
- [[ATOC_6_4] Alias Template](/4_EfectiveCplusplus/ATOC_6_Template/4_TemplateMechanisms/WhatIsAliasTemplate.md)
- [[ATOC_6_4] Compile-time selection mechanism: if constexpr](/4_EfectiveCplusplus/ATOC_6_Template/4_TemplateMechanisms/WhatIsCompileTimeSelection.md)
- [[ATOC_7_2] Concept](/4_EfectiveCplusplus/ATOC_7_ConceptAndGenericProgramming/2_Concepts/1_WhatIsConcept.md)
- [[ATOC_7_3] Generic Programming](/4_EfectiveCplusplus/ATOC_7_ConceptAndGenericProgramming/3_GenericProgramming.md)
- [[ATOC_7_4] Variadic Template?](/4_EfectiveCplusplus/ATOC_7_ConceptAndGenericProgramming/4_WhatIsVariadicTemplate.md)
- [[ATOC_7_4] Fold Expression (C++17)](/4_EfectiveCplusplus/ATOC_7_ConceptAndGenericProgramming/4_1_FoldExpression.md)
- [[ATOC_7_4] Forwarding Argument in template?](/4_EfectiveCplusplus/ATOC_7_ConceptAndGenericProgramming/4_2_ForwardingArgument.md)
- [[EC_7_GenericProgramming] 41. Implicit interfaces and Compile-time Polymorphism.](/4_EfectiveCplusplus/EC_7_TemplatesAndGenericProgramming/Item41_UnderstandImplicitInterfacesAndCompileTimePoly.md)
- [[EC_7_GenericProgramming] 42. Two meanings of typename.](/4_EfectiveCplusplus/EC_7_TemplatesAndGenericProgramming/Item42_TwoMeaningOfTypename.md)
- [[EC_7_GenericProgramming] 45. Use member functions template to accept all compatible types.](/4_EfectiveCplusplus/EC_7_TemplatesAndGenericProgramming/Item45_MemberFunctionTemplatesToAcceptAllCompatibleTypes.md)
- [[EC_7_GenericProgramming] 46: Define non-member function inside templates when type conversions are desired](/4_EfectiveCplusplus/EC_7_TemplatesAndGenericProgramming/Item46_DefineNonMemberFunctionsInsideTemplatesWhenTypeConversion.md)
- [[EC_7_GenericProgramming] 47. Traits for Information about types](/4_EfectiveCplusplus/EC_7_TemplatesAndGenericProgramming/Item47_UseTraitsClassesForInformationAboutTypes.md)


### Advanced
- [[others] Why can I return a local declared vector?](others/WhyCanIReturnLocalDeclarecVector.md)

## Reference
[1] Effective C++: 55 Specific Ways to Improve Your Programs and Designs 3rd Edition, Scott Meyers.

[2] Effective Modern C++: 42 Specific Ways to Improve Your Use of C++11 and C++14 1st Edition, Scott Meyers.

[3] A Tour of C++ (2e), Bjarne Stroustrup