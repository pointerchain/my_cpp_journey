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
 - `bool` (1 byte)
 - `char` (*ALWAYS* 1 byte)
 - `int` (4 bytes)
 - `unsigned` (4 bytes)
 - `double` (8 bytes)

> Note: These sizes are relative to compiler and system-architecture but these are by far the most common for modern systems.

All type sizes are based off of the size of *char*.

Integer literals base:
 - *Integer literals* are by default decimal (base 10).
 - A *binary* (base  2) integer literal is prefixed by `0b`.
 - A *hexadecimal* (base 16) integer is prefixed by `0x`.
 - An *octal* (base 8) integer literal is prefixed by `0`.

To make long literals more readable you can use a single quote **(')** as a digit separator.

#### Example
```cpp
int x = 11'200'456'123'445;
```

**Unspecified Evaluation Order.**

 - Within a single statement, the compiler can reorder the execution of sub-expressions or function arguments for optimization. For example, in h(f(x), g(y)), there is no guarantee that f(x) will run before g(y).
 - This can become problematic if your functions have side effects.

 You can use both `=` amd `{}` for object initialization. `=` is the old way of doing it and `{}` is the newer C++11 way of doing it.
 Using `{}` is usually more preferable to using the more traditional `=` because it is more explicit and avoids implicit narrowing conversions (int i {7.8} // Error).
 - When using `auto` always use `=`. This avoid type declaration confusion.
 - For class constructors with args use `()`. This avoids `std::initializer_list` "*gotchas*".

 A declaration introduces its name into a scope:
  - *Local Scope* (A name declared in a function is called a `local name`).
  - *Class Scope (A name is called a `member name` if it is defined in a class).
  - *Namespace Scope* (A name is called a `namespace member name` if it is defined in a namespace).
  - A name not declared inside of any other construct is called a `global name`.
  - In addition, we can also have objects without names, such as `temporaries` and objects created using `new`.

An object must be `constructed` (initialized) before it is used.
An object will be `destroyed` at the *end of its scope*.
For a namespace object the point of `destruction` is the *end of the program*.
An object created by `new` *lives* until destroyed by *delete*

`constexpr` variable is a constant that must be able to be evaluated at compile time.
When `constexpr` is used for functions (constexpr int foo()) it does not mean that it can't be used for non-constant-expressions, but it gives it the capability to be used in a constant-expression. When want a function that can only be used for evaluation at compile time we use `consteval`

`*`, `&`, `[]`, and `()` are declarator operators whn used in declarations.

We cane advance a pointer to pointer to the next element of an array using `++`.
We can leave out the initializer in a for-statement if we don't need it
#### Example
```cpp
for (; *p!= 0; ++p) {}
```

```cpp
if (*p) {} // Where *p is a numeric value is equivalent to saying (if (*p != 0))
if (p) {}  // us equivalent to saying (if (p != nullptr))
```