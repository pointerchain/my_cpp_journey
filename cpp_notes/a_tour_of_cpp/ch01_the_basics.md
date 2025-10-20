# A Tour of C++
## Chapter 1: The Basics

**Source Files** are **Compiled** into **Object Files** then **Linked** together yielding an **Executable File**

When we talk about *portability* of C++ programs, we usually mean portability of the *source code*.

The ISO C++ Standard defines two kinds of entities.
 - *Core language features*, such as built-in types and loops.
 - *Standard library components*, such as containers and I/O operations,

**Types** are the *basic vocabulary* of **Data**, **Functions** and **Classes** are the *basic vocabulary* of **Computation**

When a function is *overloaded*, each function of the same name should implement the same *semantics*.

A *declaration* is a statement that introduce an entity into the program and specifies its type.
 - A *type* defines a set of possible values and a set of operations (for an object).
 - An *object* is some memory that holds a value of some type.
 - A *value* is a set of bits interpreted according to a type.

> Note: This definition of object is a technical one, another more standard definition of object means an instance of a class.

Byte sizes:
 - bool (1 byte)
 - char (1 byte)
 - int (4 bytes)
 - unsigned (4 bytes)
 - double (8 bytes)

 > Note: These sizes are relative to compiler and system-architecture but these are by far the most common for modern systems.