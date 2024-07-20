# The preprocessor in C and C++

The preprocessor in C and C++ was introduced to provide a mechanism for code manipulation before actual compilation. It performs text substitution and macro expansion, allowing developers to define constants, macros, and perform conditional compilation. The preprocessor directives start with a `#` symbol and are processed before the actual compilation of the code begins.

## Reasons for Introduction

### Macro Definitions
The preprocessor allows you to define macros using the `#define` directive. Macros are used for code replacement, providing a way to define constants or to create reusable code snippets. For example:

```cpp
#define PI 3.14159
```

After this definition, every occurrence of `PI` in the code will be replaced by `3.14159`.

### Header Files
The preprocessor is used to include header files in the source code using the `#include` directive. Header files contain declarations and definitions that are shared across multiple source files. This promotes modular programming and code reuse.

```cpp
#include <iostream>
```

### Conditional Compilation
The preprocessor allows you to include or exclude parts of the code based on conditional statements using `#if`, `#ifdef`, `#ifndef`, `#else`, `#elif`, and `#endif`. This is useful for creating code that can adapt to different compilation conditions.

```cpp
#ifdef DEBUG
// Debugging code here
#endif
```

### File Inclusion and Redirection
The preprocessor provides directives like `#include` and `#define` to manage the inclusion of files and to control the flow of compilation. This allows for the creation of modular and reusable code.

```cpp
#include "myheader.h"
```

### Conditional Compilation (Repeated)
The preprocessor allows you to include or exclude parts of the code based on conditional statements using `#if`, `#ifdef`, `#ifndef`, `#else`, `#elif`, and `#endif`. This is useful for creating code that can adapt to different compilation conditions.

```cpp
#ifdef DEBUG
// Debugging code here
#endif
```

### Line Control
The `#line` directive allows you to control the line numbers reported by the compiler. This can be helpful for debugging and error reporting.

```cpp
#line 100 "myfile.cpp"
```

It's important to note that while the preprocessor provides powerful capabilities, excessive use of macros and conditional compilation can make the code more difficult to understand and maintain. Therefore, it's recommended to use these features judiciously and consider alternatives, such as inline functions and const variables, where appropriate.

# Different forms of initialization

Initialization in C++ is surprisingly complex, so we’ll present a simplified view here.

There are 6 basic ways to initialize variables in C++:

```C++
int a;         // no initializer (default initialization)
int b = 5;     // initial value after equals sign (copy initialization)
int c( 6 );    // initial value in parenthesis (direct initialization)

// List initialization methods (C++11) (preferred)
int d { 7 };   // initial value in braces (direct list initialization)
int e = { 8 }; // initial value in braces after equals sign (copy list initialization)
int f {};      // initializer is empty braces (value initialization)
```


# `[[maybe_unused]]` Attribute

`[[maybe_unused]]` is an attribute introduced in C++17 that indicates to the compiler that a variable, function, or parameter might be intentionally unused. This attribute suppresses compiler warnings about unused entities, helping to improve code readability and maintainability. Here's an overview of `[[maybe_unused]]`:

### 1. Syntax:
   - `[[maybe_unused]]` is placed before the declaration of a variable, function, or parameter.
   - Example usage:
     ```cpp
     [[maybe_unused]] int x; // Unused variable
     void foo([[maybe_unused]] int param) { // Unused parameter
         // Function body
     }
     ```

### 2. Purpose:
   - The purpose of `[[maybe_unused]]` is to inform the compiler that a particular entity may intentionally remain unused in the code.
   - It suppresses compiler warnings about unused entities, reducing noise in compiler output and emphasizing intentional design choices.

### 3. Use Cases:
   - **Unused Variables:** Use `[[maybe_unused]]` for variables that are declared but might not be used in the code.
   - **Unused Parameters:** Use `[[maybe_unused]]` for function parameters that are not used within the function body.

### 4. Benefits:
   - **Clarity:** Clearly communicates the developer's intention to potentially leave certain entities unused.
   - **Maintainability:** Helps prevent accidental removal of code that might be necessary in the future.
   - **Compiler Warnings:** Suppresses compiler warnings about unused entities, reducing noise during compilation.

### 5. Compatibility:
   - `[[maybe_unused]]` is supported by C++17-compliant compilers and later versions.
   - It is backward-compatible with older compilers that do not recognize the attribute, as it is treated as a standard comment.

### 6. Example:
   ```cpp
   #include <iostream>

   [[maybe_unused]] int calculate() {
       // Function body
       return 42;
   }

   int main() {
       [[maybe_unused]] int result = calculate(); // Unused variable
       return 0;
   }
```

# Everything About Const Variables in C++

In C++, a `const` variable is a variable whose value cannot be changed once it has been initialized. Here's a comprehensive overview of const variables in C++:

### 1. Declaration and Initialization:
   - In C++, a `const` variable is declared using the `const` keyword followed by the data type and the variable name.
   - A `const` variable must be initialized at the time of declaration.

     ```cpp
     const int MAX_VALUE = 100;
     ```

### 2. Benefits:
   - **Safety:** `const` variables prevent accidental modification of values, enhancing code safety.
   - **Readability:** They improve code readability by clearly indicating that certain values should not change.
   - **Compiler Optimization:** Const variables can enable certain compiler optimizations.

### 3. Global Const Variables:
   - `const` variables can be declared at the global scope, providing constants that are accessible across multiple translation units.
   - Typically, global `const` variables are declared in header files and defined in source files to avoid multiple definitions.

     ```cpp
     // Header file (declaration)
     extern const double PI;

     // Source file (definition)
     const double PI = 3.14159;
     ```

### 4. Const and Pointers:
   - `const` can be applied to pointers to indicate whether the pointed-to data is constant or whether the pointer itself is constant.
   - `const` pointer: Pointer itself is constant.
   - Pointer to `const`: Pointed-to data is constant.
   - `const` pointer to `const`: Both pointer and pointed-to data are constant.

     ```cpp
     const int* ptr1;       // Pointer to a constant integer
     int const* ptr2;       // Same as above
     int* const ptr3;       // Constant pointer to an integer
     const int* const ptr4; // Constant pointer to a constant integer
     ```

### 5. Const Member Functions:
   - In class declarations, `const` can be used to indicate that a member function does not modify the object's state.
   - Const member functions can be called on `const` objects but not on non-`const` objects.

     ```cpp
     class MyClass {
     public:
         void regularFunction();
         void constFunction() const; // Const member function
     };
     ```

### 6. Constexpr Constants:
   - In modern C++, constants can be declared using `constexpr`, allowing them to be computed at compile time.
   - `constexpr` variables must be initialized with constant expressions known at compile time.

     ```cpp
     constexpr double PI = 3.14159;
     ```

### 7. Enumerations:
   - Enumerations in C++ can act as a form of constant variables, with explicit values assigned to them.
   - Enumerations can provide symbolic names for integer values, improving code readability and maintainability.

     ```cpp
     enum Days { SUNDAY = 0, MONDAY = 1, /* ... */ };
     ```

### 8. Const in Function Signatures:
   - `const` can be used in function signatures to indicate that the function does not modify its parameters.
   - This helps enforce the function's contract and prevents unintended modifications of function arguments.

     ```cpp
     void printValue(const int& value);
     ```

### 9. Const_cast:
   - `const_cast` is a way to temporarily remove the `const` qualifier from a variable.
   - It should be used with caution to avoid violating the true constness of the variable.

     ```cpp
     const int x = 5;
     int& y = const_cast<int&>(x);
     ```

### 10. Const Overloading:
   - Multiple overloaded versions of a function can exist, where one is for `const` objects and the other is for non-`const` objects.
   - This allows for different behavior based on whether the object is `const` or non-`const`.

     ```cpp
     class MyClass {
     public:
         void display() const;    // For const objects
         void display();          // For non-const objects
     };
     ```

### 11. Template Metaprogramming:
   - Const expressions are often used in conjunction with templates to perform metaprogramming, where computations are performed at compile time rather than runtime.

### 12. Performance Considerations:
   - Const variables may enable certain compiler optimizations, leading to potential performance improvements.
   - However, excessive use of `const` may lead to code verbosity and decreased readability.

Understanding and appropriately using `const` variables in C++ can lead to safer, more maintainable, and optimized code. They play a crucial role in expressing program semantics and intentions, especially in the context of immutability and const-correctness.

# Everything You Should Know About `constexpr`

`constexpr` is a powerful feature introduced in C++11 and enhanced in subsequent standards (C++14, C++17, C++20) to support compile-time evaluation of expressions. It allows you to specify that the value of a variable or function can be computed at compile time. Here's everything you should know about `constexpr`:

### 1. **Compile-Time Evaluation:**
   - `constexpr` allows certain computations to be performed at compile time rather than at runtime, thus improving performance and enabling optimizations.

### 2. **`constexpr` Variables:**
   - Variables declared with `constexpr` must be initialized with constant expressions known at compile time.
   - These variables are implicitly `const`, meaning their values cannot be changed.

     ```cpp
     constexpr int size = 10;
     ```

### 3. **`constexpr` Functions:**
   - Functions declared with `constexpr` can be evaluated at compile time if their arguments are known at compile time.
   - These functions can be called in contexts that require constant expressions.

     ```cpp
     constexpr int square(int x) {
         return x * x;
     }
     ```

### 4. **Constraints on `constexpr` Functions:**
   - `constexpr` functions must have a return type that is literal, and their bodies must consist of exactly one return statement.
   - The parameters and return type of `constexpr` functions must be literal types, such as built-in types and certain user-defined types.

### 5. **Use Cases:**
   - `constexpr` is useful for defining constants, such as mathematical constants or sizes of arrays, at compile time.
   - It enables the creation of more efficient code by computing values at compile time rather than runtime.
   - `constexpr` functions can be used to perform computations on types known at compile time, such as template metaprogramming.

### 6. **`constexpr` Constructors:**
   - In C++11, constructors of literal types can be declared as `constexpr`. This allows objects of these types to be initialized at compile time.

### 7. **Improvements in C++14:**
   - In C++14, `constexpr` functions can contain a broader set of operations, including conditional statements (`if`, `switch`), loops (`for`, `while`), and more.
   - The restrictions on `constexpr` functions were relaxed, making it easier to write complex compile-time computations.

### 8. **Runtime Evaluation:**
   - If a `constexpr` function is called with arguments known only at runtime, it behaves like a regular function and is evaluated at runtime.

### 9. **String Literals:**
   - In C++11, string literals are not `constexpr`, but in C++14, they can be used as `constexpr` in certain contexts.

### 10. **`constexpr` and Standard Library:**
   - Many standard library functions and types have been updated to support `constexpr`, allowing their use in compile-time computations.

### 11. **`constexpr` Lambdas:**
   - C++20 introduced the ability to declare lambdas as `constexpr`, allowing for compile-time evaluation of lambda expressions.

### 12. **Debugging `constexpr` Code:**
   - Debugging `constexpr` code can be challenging because compiler errors and warnings may not be as informative as those for regular code. It's essential to understand compiler messages and be aware of potential pitfalls.

### 13. **Template Metaprogramming:**
   - `constexpr` is often used in conjunction with templates to perform metaprogramming, where computations are performed at compile time rather than runtime.

### 14. **Performance Considerations:**
   - While `constexpr` can improve performance by moving computations to compile time, excessive use of complex `constexpr` functions may increase compilation times.

Understanding `constexpr` and leveraging it appropriately can lead to more efficient and maintainable C++ code, especially in contexts where compile-time evaluation is desirable.

# Comparison between `const` and `constexpr`

### 1. Purpose:
   - **`const`:** Used to declare variables with values that cannot be changed after initialization.
   - **`constexpr`:** Used to declare variables or functions whose values can be computed at compile time.

### 2. Usage:
   - **`const`:** 
     - Applied to variables to indicate immutability.
     - Can be used with pointers, member functions, and global variables.
     - Initialized at runtime.
   
   - **`constexpr`:**
     - Applied to variables or functions.
     - Variables must be initialized with constant expressions known at compile time.
     - Functions must have a literal return type and consist of a single return statement.

### 3. Compile-Time Evaluation:
   - **`const`:** Values are determined at runtime.
   - **`constexpr`:** Values can be computed at compile time if their arguments are known at compile time.

### 4. Performance:
   - **`const`:** Does not provide compile-time evaluation, so no compile-time performance benefits.
   - **`constexpr`:** Enables certain computations to be performed at compile time, potentially improving performance.

### 5. Examples:
   - **`const`:** 
     ```cpp
     const int MAX_VALUE = 100;
     ```

   - **`constexpr`:**
     ```cpp
     constexpr double PI = 3.14159;
     
     constexpr int square(int x) {
         return x * x;
     }
     ```

### 6. Usage Scenarios:
   - **`const`:** Used for values that are known and fixed at runtime, such as configuration values or function parameters that should not be modified.
   - **`constexpr`:** Used for values or functions that can be evaluated at compile time, such as mathematical constants, array sizes, or template metaprogramming.

### 7. Compatibility:
   - **`const`:** Supported in all versions of C++.
   - **`constexpr`:** Introduced in C++11 and enhanced in subsequent standards (C++14, C++17, C++20).


# Everything About `consteval`

`consteval` is a feature introduced in C++20 to specify that a function or constructor must be evaluated at compile time. Here's a comprehensive overview of `consteval`:

### 1. **Compile-Time Evaluation:**
   - `consteval` indicates that a function or constructor must be evaluated at compile time.
   - This ensures that the function or constructor is called only with constant expressions known at compile time.

### 2. **Declaration:**
   - `consteval` is used as a specifier before function or constructor declarations.
   - It precedes the return type or constructor name.

### 3. **Use Cases:**
   - **Compile-Time Computations:** `consteval` is suitable for functions and constructors where the computation can be performed entirely at compile time.
   - **Compile-Time Validation:** It is useful for performing compile-time checks or validation, ensuring that certain conditions are met at compile time.

### 4. **Benefits:**
   - **Performance:** Compile-time evaluation can lead to performance improvements by eliminating runtime computations.
   - **Error Detection:** Compile-time evaluation helps detect errors early in the development process, preventing runtime errors related to incorrect or invalid expressions.

### 5. **Constraints:**
   - `consteval` functions and constructors must be invoked with constant expressions known at compile time.
   - They must consist of a single return statement or a constructor initializer list.
   - Recursive `consteval` calls are not allowed.

### 6. **Syntax:**
   - Syntax for `consteval` function:
     ```cpp
     consteval int square(int x) {
         return x * x;
     }
     ```

   - Syntax for `consteval` constructor:
     ```cpp
     struct MyClass {
         consteval MyClass(int x) : value(x) {}
         int value;
     };
     ```

### 7. **Difference from `constexpr`:**
   - `consteval` functions and constructors must be evaluated at compile time, whereas `constexpr` allows runtime evaluation if necessary.
   - `consteval` enforces compile-time evaluation strictly, providing stronger guarantees than `constexpr`.

### 8. **Example:**
   ```cpp
   consteval int factorial(int n) {
       return (n <= 1) ? 1 : n * factorial(n - 1);
   }
   ```

### 9. Usage Considerations:
  - Use `consteval` for functions and constructors that must be evaluated at compile time.
  - Ensure that the expressions passed to `consteval` functions are known at compile time to avoid runtime evaluation.
  - `consteval` provides a powerful mechanism for performing computations and validations at compile time, leading to improved performance and enhanced safety in C++ programs.

`consteval` provides a powerful mechanism for performing computations and validations at compile time, leading to improved performance and enhanced safety in C++ programs.

This has good explaination on `constexpr` and `consteval` - [https://www.learncpp.com/cpp-tutorial/constexpr-and-consteval-functions](https://www.learncpp.com/cpp-tutorial/constexpr-and-consteval-functions/)

# Everything About `std::string`

`std::string` is a part of the Standard Template Library (STL) in C++ and is a class that represents a sequence of characters. It provides a convenient way to work with strings in C++, offering various functionalities for string manipulation.

### 1. Include Directive:
   - To use `std::string`, include the `<string>` header file in your C++ program.
     ```cpp
     #include <string>
     ```

### 2. Declaration and Initialization:
   - You can declare and initialize `std::string` objects in several ways:
     ```cpp
     std::string str1;                 // Default-initialized (empty) string
     std::string str2 = "Hello";       // Initialized with a string literal
     std::string str3("World");        // Initialized with constructor
     std::string str4(str2);           // Copy-initialized from another string
     ```

### 3. Basic Operations:
   - `std::string` supports various operations such as concatenation, comparison, and access to individual characters.
     ```cpp
     str1 = str2 + str3;               // Concatenation
     bool equal = (str1 == str2);      // Comparison
     char ch = str1[0];                // Accessing individual characters
     ```

### 4. String Length:
   - You can get the length of a string using the `length()` or `size()` member functions.
     ```cpp
     size_t len = str1.length();       // Length of the string
     ```

### 5. String Iterators:
   - `std::string` provides iterators to traverse the characters in a string.
     ```cpp
     for(auto it = str1.begin(); it != str1.end(); ++it) {
         // Process each character
     }
     ```

### 6. String Operations:
   - `std::string` supports various operations such as finding substrings, replacing characters, and converting to/from C-style strings.
     ```cpp
     size_t pos = str1.find("world");          // Find a substring
     str1.replace(pos, 5, "planet");            // Replace characters
     const char* cstr = str1.c_str();          // Convert to C-style string
     ```

### 7. Input and Output:
   - You can input/output `std::string` objects using standard stream operators (`>>` and `<<`).
     ```cpp
     std::cout << str1 << std::endl;           // Output a string
     std::cin >> str2;                          // Input a string
     ```

### 8. Memory Management:
   - `std::string` manages memory dynamically, automatically resizing as necessary to accommodate the stored characters.
   - It abstracts away memory management details, providing a convenient and safe interface for working with strings.

### 9. Performance Considerations:
   - `std::string` provides efficient operations for most common string manipulations, but excessive copying and concatenation may lead to performance overhead.
   - Use functions like `reserve()` to preallocate memory if the string size is known in advance to avoid unnecessary reallocations.

### 10. Compatibility:
   - `std::string` is compatible with C-style strings (`const char*`), allowing interoperability with functions that expect null-terminated character arrays.

### 11. Usage Guidelines:
   - Prefer using `std::string` over C-style strings (`const char*`) for safer and more convenient string manipulation.
   - Be mindful of memory allocations and consider performance implications when working with large strings or performing intensive string operations.

`std::string` provides a versatile and efficient way to work with strings in C++, offering a wide range of functionalities for string manipulation and management.

This overview covers the essential aspects of `std::string` in C++, including declaration, initialization, basic operations, string length, iterators, string operations, input/output, memory management, performance considerations, compatibility, and usage guidelines.

# Difference Between `std::string` and `std::string_view`

`std::string` and `std::string_view` are both used for representing strings in C++, but they have different characteristics and purposes. Here's a comparison between the two:

### 1. Ownership:
- **`std::string`:** Owns its data and manages memory dynamically. It has its own copy of the string data.
- **`std::string_view`:** Does not own its data. It is a non-owning view of an existing string, either a `std::string` or a C-style string (`const char*`). It does not manage memory.

### 2. Mutability:
- **`std::string`:** Mutable. You can modify the contents of a `std::string`.
- **`std::string_view`:** Immutable. You cannot modify the contents of a `std::string_view`. It provides read-only access to the underlying string data.

### 3. Memory Management:
- **`std::string`:** Dynamically allocates and manages memory for its contents. It automatically handles memory allocation and deallocation.
- **`std::string_view`:** Does not perform memory allocation. It simply refers to an existing string data without any memory management.

### 4. Performance:
- **`std::string`:** Can involve memory allocation and copying of data, which may have performance implications, especially for large strings.
- **`std::string_view`:** Lightweight and efficient. It does not involve memory allocation or copying, making it suitable for passing around string data without overhead.

### 5. Usage Scenarios:
- **`std::string`:** Use when you need to own and modify string data or when dynamic memory management is required.
- **`std::string_view`:** Use when you want to refer to existing string data without copying or when you need a read-only view of a string.

### 6. Safety:
- **`std::string`:** Provides safety through memory management but may involve unnecessary copying.
- **`std::string_view`:** Provides safety by avoiding unnecessary copying and allowing only read access, but it relies on the underlying string data to remain valid.

### 7. Compatibility:
- **`std::string`:** Provides compatibility with functions and APIs that expect a mutable, null-terminated string.
- **`std::string_view`:** Provides compatibility with functions and APIs that accept a read-only view of string data.

### 8. Example:
```cpp
std::string str = "Hello";
std::string_view view = str;

// Mutating the original string
str += " World";

// Contents of the string view remain unchanged
std::cout << view; // Output: "Hello"
```

# Notes on `std::bitset`

- `std::bitset` is a C++ class template for representing a fixed-size sequence of bits.
- Useful for bitwise operations and efficient bit manipulation.
- Header to include: `<bitset>`.

## Declaration
- Declare a bitset with a specified number of bits:
  ```cpp
  std::bitset<8> bits;  // 8-bit bitset
  ```
## Initialization
- Default Initialization: All bits are initialized to 0.
   ```cpp
   std::bitset<8> bits;  // 00000000
   ```
- From an unsigned integer: Initializes the bitset from an unsigned integer.
   ```cpp
   std::bitset<8> bits(42);  // 00101010
   ```
- From a string: Initializes the bitset from a string of 0s and 1s.
   ```cpp
   std::bitset<8> bits("1100");  // 00001100
   ```
- Accessing Bits: Use the [] operator to access and manipulate individual bits:
   ```cpp
   std::bitset<8> bits(42);
   bool bit = bits[1];  // Accesses the second bit (true)
   bits[0] = 1;        // Sets the first bit
   ```
## Methods

Example
```cpp
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> bits("1100");

    std::cout << "Initial bitset: " << bits << std::endl;

    bits.set(1);
    std::cout << "After setting bit 1: " << bits << std::endl;

    bits.reset(2);
    std::cout << "After resetting bit 2: " << bits << std::endl;

    bits.flip(3);
    std::cout << "After flipping bit 3: " << bits << std::endl;

    std::cout << "Any bits set? " << bits.any() << std::endl;
    std::cout << "None bits set? " << bits.none() << std::endl;
    std::cout << "All bits set? " << bits.all() << std::endl;
    std::cout << "Number of bits set: " << bits.count() << std::endl;

    std::cout << "Bitset as string: " << bits.to_string() << std::endl;
    std::cout << "Bitset as unsigned long: " << bits.to_ulong() << std::endl;

    std::bitset<8> a("1100");
    std::bitset<8> b("1010");

    std::cout << "a & b: " << (a & b) << std::endl;
    std::cout << "a | b: " << (a | b) << std::endl;
    std::cout << "a ^ b: " << (a ^ b) << std::endl;
    std::cout << "~a: " << ~a << std::endl;

    std::cout << "a << 2: " << (a << 2) << std::endl;
    std::cout << "a >> 2: " << (a >> 2) << std::endl;

    return 0;
}
```

# Variable shadowing (name hiding)
Each block defines its own scope region. So what happens when we have a variable inside a nested block that has the same name as a variable in an outer block? When this happens, the nested variable “hides” the outer variable in areas where they are both in scope. This is called name hiding or shadowing.

```cpp
#include <iostream>

int main()
{ // outer block
    int apples{5}; // here's the outer block apples

    { // nested block
        // apples refers to outer block apples here
        std::cout << apples << '\n'; // print value of outer block apples

        // no inner block apples defined in this example

        apples = 10; // this applies to outer block apples

        std::cout << apples << '\n'; // print value of outer block apples
    } // outer block apples retains its value even after we leave the nested block

    std::cout << apples << '\n'; // prints value of outer block apples

    return 0;
} // outer block apples destroyed
```

```cpp
#include <iostream>
int value { 5 }; // global variable

int main()
{
    int value { 7 }; // hides the global variable value
    ++value; // increments local value, not global value

    --(::value); // decrements global value, not local value (parenthesis added for readability)

    std::cout << "local variable value: " << value << '\n';
    std::cout << "global variable value: " << ::value << '\n';

    return 0;
} // local value is destroyed
```

# C++11 Random Library

## Introduction

The C++11 standard introduced a new random library, which provides a more robust and flexible way of generating random numbers. This library is a significant improvement over the traditional `rand()` function and provides a more modern and efficient way of generating random numbers.

## Header File

The random library is included in the `<random>` header file.

## Classes and Functions

The random library provides several classes and functions for generating random numbers. The main classes and functions are:

### `std::random_device`

- A non-deterministic random number generator.
- Uses external sources of randomness, such as hardware devices.
- Provides a truly random sequence of numbers.

### `std::mt19937`

- A Mersenne Twister random number generator.
- A widely used and highly regarded algorithm for generating random numbers.
- Provides a high-quality sequence of random numbers.

### `std::uniform_int_distribution`

- A distribution class that generates a uniform distribution of integers.
- Provides a way to generate random numbers within a specific range.

### `std::uniform_real_distribution`

- A distribution class that generates a uniform distribution of floating-point numbers.
- Provides a way to generate random numbers within a specific range.

### `std::normal_distribution`

- A distribution class that generates a normal distribution of numbers.
- Provides a way to generate random numbers with a mean and standard deviation.

### Example Usage

Here is an example of how to use the C++11 random library:

```cpp
#include <random>
#include <iostream>

int main() {
  // Create a random device
  std::random_device rd;

  // Create a Mersenne Twister generator
  std::mt19937 gen(rd());

  // Create a uniform distribution of integers
  std::uniform_int_distribution<> dis(1, 10);

  // Generate 10 random numbers
  for (int i = 0; i < 10; i++) {
    std::cout << dis(gen) << " ";
  }
  return 0;
}
```

### Advantages

- Provides a more robust and flexible way of generating random numbers.
- Provides a non-deterministic random number generator.
- Provides high-quality random number generators.
- Provides a way to generate random numbers with specific distributions.

### Notes

- The `std::random_device` class is not available on all platforms.
- The `std::mt19937 class` is a widely used and highly regarded algorithm, but it is not suitable for cryptographic purposes.
- The random library provides other classes and functions for generating random numbers, such as `std::poisson_distribution` and `std::exponential_distribution`.

# Type Conversion

Type conversion, also known as type casting, is the process of converting a value of one data type to another. There are two types of type conversion:

## Implicit Type Conversion

Implicit type conversion, also known as automatic type conversion, occurs automatically without the need for a cast. For example:

```cpp
int x = 5;
double y = x;  // implicit conversion from int to double
```

## Explicit Type Conversion

Explicit type conversion, also known as casting, requires a cast operator. There are several types of explicit casts:

### Static Cast

`static_cast` is used for explicit type conversion between related types, such as casting a derived class to its base class. It performs a compile-time check to ensure the cast is safe. For example:

```cpp
class Animal { ... };
class Dog : public Animal { ... };

Dog myDog;
Animal* animalPtr = static_cast<Animal*>(&myDog);  // safe downcast
```

### Dynamic Cast

`dynamic_cast` is used for explicit type conversion between related types, similar to static_cast, but it performs a runtime check to ensure the cast is safe. For example:

```cpp
class Animal { ... };
class Dog : public Animal { ... };

Animal* animalPtr = new Dog;
Dog* dogPtr = dynamic_cast<Dog*>(animalPtr);  // runtime check
```

### Reinterpret Cast

`reinterpret_cast` is used for low-level, unsafe type conversion, such as casting between unrelated types or casting a pointer to an integer. It should be used with caution. For example:

```cpp
int x = 5;
double y = reinterpret_cast<double&>(x);  // unsafe cast
```

### Const Cast

`const_cast` is used to cast away the const qualifier from a variable. It is used when you need to modify a variable that is initially declared as const. For example:

```cpp
const int x = 5;
int& y = const_cast<int&>(x);  // cast away const
```

# Type Aliases

Type aliases, introduced in C++11, allow you to create alternative names for existing types. They are defined using the using keyword. For example:

```cpp
using MyInt = int;  // create a type alias for int
MyInt x = 5;  // equivalent to int x = 5;
```

# Type Deduction

Type deduction, introduced in C++11, allows the compiler to automatically deduce the type of a variable or expression. It is used in various contexts, including:

## Auto Keyword

The auto keyword allows the compiler to deduce the type of a variable. For example:

```cpp
auto x = 5;  // x is deduced to be of type int
```

When using an `auto` return type (introduced in C++14), all return statements within the function must return values of the same type, otherwise an error will result. For example:

```cpp
auto someFcn(bool b)
{
    if (b)
        return 5; // return type int
    else
        return 6.7; // return type double
}
```
In the above function, the two return statements return values of different types, so the compiler will give an error.

## Template Argument Deduction

Template argument deduction allows the compiler to deduce the types of template arguments. For example:

```cpp
template <typename T>
void func(T x) { ... }

func(5);  // T is deduced to be int
```

## decltype Keyword

The `decltype` keyword allows the compiler to deduce the type of an expression. For example:

```cpp
int x = 5;
decltype(x) y = x;  // y is deduced to be of type int
```


