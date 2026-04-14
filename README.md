# C++ Complete Reference Guide

> A full reference document covering C++ from basics to advanced — syntax, concepts, patterns, and best practices.

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Program Structure](#2-program-structure)
3. [Data Types & Variables](#3-data-types--variables)
4. [Operators](#4-operators)
5. [Control Flow](#5-control-flow)
6. [Functions](#6-functions)
7. [Arrays & Strings](#7-arrays--strings)
8. [Pointers & References](#8-pointers--references)
9. [Object-Oriented Programming](#9-object-oriented-programming)
10. [Inheritance & Polymorphism](#10-inheritance--polymorphism)
11. [Templates](#11-templates)
12. [STL (Standard Template Library)](#12-stl-standard-template-library)
13. [Memory Management](#13-memory-management)
14. [Exception Handling](#14-exception-handling)
15. [File I/O](#15-file-io)
16. [Modern C++ (C++11/14/17/20)](#16-modern-c-c111417-20)
17. [Concurrency & Multithreading](#17-concurrency--multithreading)
18. [Best Practices & Common Mistakes](#18-best-practices--common-mistakes)

---

## 1. Introduction

C++ is a general-purpose, compiled, statically-typed programming language created by **Bjarne Stroustrup** in 1979 as an extension of C. It supports:

- **Procedural programming** (like C)
- **Object-Oriented Programming (OOP)**
- **Generic programming** (templates)
- **Low-level memory manipulation**

### C++ Standards Timeline

| Standard | Year | Key Features |
|----------|------|--------------|
| C++98 | 1998 | First ISO standard |
| C++03 | 2003 | Bug fixes |
| C++11 | 2011 | auto, lambdas, move semantics, smart pointers |
| C++14 | 2014 | Generic lambdas, constexpr improvements |
| C++17 | 2017 | std::optional, std::variant, structured bindings |
| C++20 | 2020 | Concepts, ranges, coroutines, modules |
| C++23 | 2023 | std::print, std::expected, more ranges |

### Compiling a C++ Program

```bash
# GCC
g++ -std=c++17 -o output main.cpp

# Clang
clang++ -std=c++17 -o output main.cpp

# With warnings (recommended)
g++ -std=c++17 -Wall -Wextra -o output main.cpp
```

---

## 2. Program Structure

### Hello World

```cpp
#include <iostream>   // Include standard I/O library

int main() {          // Entry point of every C++ program
    std::cout << "Hello, World!" << std::endl;
    return 0;         // 0 means success
}
```

### Using Namespace

```cpp
#include <iostream>
using namespace std;  // Avoid typing std:: everywhere (not recommended in headers)

int main() {
    cout << "Hello!" << endl;
    return 0;
}
```

### Preprocessor Directives

```cpp
#include <iostream>       // Include standard library header
#include "myfile.h"       // Include local header

#define PI 3.14159        // Macro constant
#define SQUARE(x) ((x)*(x)) // Macro function (prefer constexpr instead)

#ifdef DEBUG
    cout << "Debug mode" << endl;
#endif

#pragma once              // Include guard (modern alternative to #ifndef guards)
```

### Header Guards (traditional)

```cpp
// myheader.h
#ifndef MYHEADER_H
#define MYHEADER_H

// declarations here

#endif // MYHEADER_H
```

---

## 3. Data Types & Variables

### Fundamental Types

```cpp
// Integer types
int a = 42;                  // typically 32-bit
short b = 100;               // at least 16-bit
long c = 100000L;            // at least 32-bit
long long d = 9999999999LL;  // at least 64-bit

// Unsigned variants
unsigned int ua = 42u;
unsigned long long ull = 100ULL;

// Floating point
float f = 3.14f;             // ~7 decimal digits precision
double d2 = 3.14159265358;   // ~15 decimal digits precision
long double ld = 3.14L;      // extended precision

// Character
char ch = 'A';               // 1 byte
wchar_t wch = L'A';          // wide character
char16_t c16 = u'A';         // UTF-16
char32_t c32 = U'A';         // UTF-32

// Boolean
bool flag = true;            // true or false

// Void
void myFunc() {}             // no return value
```

### Fixed-Width Types (from `<cstdint>`)

```cpp
#include <cstdint>

int8_t   a;   // exactly 8-bit signed
int16_t  b;   // exactly 16-bit signed
int32_t  c;   // exactly 32-bit signed
int64_t  d;   // exactly 64-bit signed

uint8_t  ua;  // exactly 8-bit unsigned
uint16_t ub;
uint32_t uc;
uint64_t ud;
```

### Variable Declaration & Initialization

```cpp
int x;           // declared (undefined value — dangerous)
int y = 10;      // copy initialization
int z(10);       // direct initialization
int w{10};       // uniform/brace initialization (C++11, preferred)
int v{};         // zero-initialized

auto a = 42;     // type deduced as int
auto b = 3.14;   // type deduced as double
auto c = 'A';    // type deduced as char
auto d = true;   // type deduced as bool
```

### Constants

```cpp
const int MAX = 100;           // runtime constant, cannot be modified
constexpr int SIZE = 256;      // compile-time constant (C++11)
constexpr double PI = 3.14159265358979;

// constexpr function (evaluated at compile time if possible)
constexpr int square(int x) { return x * x; }
constexpr int s = square(5);   // computed at compile time
```

### Type Modifiers & Qualifiers

```cpp
const int x = 5;         // cannot modify
volatile int sensor;     // can change unexpectedly (hardware/ISR)
mutable int counter;     // can be modified even in const objects (inside class)
```

### Type Conversions

```cpp
// Implicit conversion
int i = 3.7;              // truncates to 3 (narrowing)

// C-style cast (avoid)
double d = (double)i;

// C++ style casts (prefer these)
double d2 = static_cast<double>(i);       // safe compile-time cast
int* ip = reinterpret_cast<int*>(somePtr); // low-level bit reinterpretation
const int* cp = const_cast<const int*>(p); // add/remove const
Base* bp = dynamic_cast<Base*>(derivedPtr); // safe downcast (RTTI)
```

### sizeof & Type Info

```cpp
#include <iostream>
#include <typeinfo>

cout << sizeof(int) << endl;        // 4 (typically)
cout << sizeof(double) << endl;     // 8
cout << typeid(x).name() << endl;   // type name string
```

---

## 4. Operators

### Arithmetic

```cpp
int a = 10, b = 3;
int sum  = a + b;    // 13
int diff = a - b;    // 7
int prod = a * b;    // 30
int quot = a / b;    // 3 (integer division)
int rem  = a % b;    // 1 (modulo)

// Increment / Decrement
a++;   // post-increment (use value, then increment)
++a;   // pre-increment  (increment, then use value)
b--;
--b;
```

### Comparison & Logical

```cpp
bool eq  = (a == b);   // equal
bool neq = (a != b);   // not equal
bool gt  = (a > b);
bool lt  = (a < b);
bool gte = (a >= b);
bool lte = (a <= b);

bool both = (a > 0 && b > 0);   // logical AND
bool either = (a > 0 || b < 0); // logical OR
bool inv = !(a == b);            // logical NOT
```

### Bitwise

```cpp
int x = 0b1010;   // binary literal (C++14)
int y = 0b1100;

int and_  = x & y;    // 0b1000 — bitwise AND
int or_   = x | y;    // 0b1110 — bitwise OR
int xor_  = x ^ y;    // 0b0110 — bitwise XOR
int not_  = ~x;       // bitwise NOT
int lsh   = x << 2;   // left shift (multiply by 4)
int rsh   = x >> 1;   // right shift (divide by 2)
```

### Assignment

```cpp
int n = 5;
n += 3;   // n = n + 3
n -= 2;   // n = n - 2
n *= 4;   // n = n * 4
n /= 2;   // n = n / 2
n %= 3;   // n = n % 3
n &= 0xFF;
n |= 0x01;
n ^= 0x10;
n <<= 1;
n >>= 1;
```

### Ternary & Comma

```cpp
int max_val = (a > b) ? a : b;   // ternary

// Comma operator (rarely used)
int result = (a++, b++, a + b);  // evaluates left to right, returns last
```

### Operator Precedence (High to Low, simplified)

```
:: (scope)
() [] -> . (postfix)
++ -- + - ! ~ * & (unary)
* / %
+ -
<< >>
< <= > >=
== !=
&
^
|
&&
||
?:
= += -= ...
,
```

---

## 5. Control Flow

### if / else if / else

```cpp
int score = 85;

if (score >= 90) {
    cout << "A" << endl;
} else if (score >= 80) {
    cout << "B" << endl;
} else if (score >= 70) {
    cout << "C" << endl;
} else {
    cout << "F" << endl;
}
```

### switch

```cpp
char grade = 'B';

switch (grade) {
    case 'A':
        cout << "Excellent" << endl;
        break;
    case 'B':
        cout << "Good" << endl;
        break;
    case 'C':
        cout << "Average" << endl;
        break;
    default:
        cout << "Unknown" << endl;
        break;
}
```

### while Loop

```cpp
int i = 0;
while (i < 5) {
    cout << i << " ";
    i++;
}
// Output: 0 1 2 3 4
```

### do-while Loop

```cpp
int n;
do {
    cout << "Enter positive number: ";
    cin >> n;
} while (n <= 0);   // executes at least once
```

### for Loop

```cpp
for (int i = 0; i < 5; i++) {
    cout << i << " ";
}

// Multiple variables
for (int i = 0, j = 10; i < j; i++, j--) {
    cout << i << "," << j << " ";
}

// Infinite loop
for (;;) {
    // ...
    break;
}
```

### Range-Based for Loop (C++11)

```cpp
#include <vector>
vector<int> nums = {1, 2, 3, 4, 5};

for (int n : nums) {
    cout << n << " ";
}

// With auto and reference (preferred for large objects)
for (auto& n : nums) {
    n *= 2;   // modifies original
}

// Const reference (read-only, no copy)
for (const auto& n : nums) {
    cout << n << " ";
}
```

### break, continue, goto

```cpp
for (int i = 0; i < 10; i++) {
    if (i == 5) break;      // exit loop entirely
    if (i % 2 == 0) continue; // skip to next iteration
    cout << i << " ";
}
// Output: 1 3

// goto (avoid — leads to spaghetti code)
goto end;
cout << "This is skipped" << endl;
end:
cout << "Jumped here" << endl;
```

---

## 6. Functions

### Basic Function

```cpp
// Declaration (prototype)
int add(int a, int b);

// Definition
int add(int a, int b) {
    return a + b;
}

// Call
int result = add(3, 4);   // result = 7
```

### Default Parameters

```cpp
void greet(string name, string greeting = "Hello") {
    cout << greeting << ", " << name << "!" << endl;
}

greet("Alice");           // Hello, Alice!
greet("Bob", "Hi");       // Hi, Bob!
```

### Function Overloading

```cpp
int multiply(int a, int b) { return a * b; }
double multiply(double a, double b) { return a * b; }
int multiply(int a, int b, int c) { return a * b * c; }

multiply(2, 3);           // calls int version
multiply(2.0, 3.0);       // calls double version
multiply(2, 3, 4);        // calls 3-param version
```

### Pass by Value, Reference, Pointer

```cpp
void byValue(int x) {
    x = 100;   // local copy modified, original unchanged
}

void byReference(int& x) {
    x = 100;   // modifies original
}

void byPointer(int* x) {
    *x = 100;  // modifies original via dereference
}

int n = 5;
byValue(n);       // n still 5
byReference(n);   // n is now 100
byPointer(&n);    // n is now 100
```

### Returning Multiple Values

```cpp
#include <tuple>
#include <utility>

// Using pair
pair<int, int> minmax(vector<int>& v) {
    return {*min_element(v.begin(), v.end()),
            *max_element(v.begin(), v.end())};
}
auto [mn, mx] = minmax(vec);   // structured binding (C++17)

// Using tuple
tuple<int, double, string> getData() {
    return {42, 3.14, "hello"};
}
auto [i, d, s] = getData();
```

### Inline Functions

```cpp
inline int square(int x) {
    return x * x;
}
// Compiler may substitute function body at call site — avoids function call overhead
```

### Recursive Functions

```cpp
int factorial(int n) {
    if (n <= 1) return 1;          // base case
    return n * factorial(n - 1);   // recursive call
}

int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

### Lambda Functions (C++11)

```cpp
// Syntax: [capture](params) -> return_type { body }

auto add = [](int a, int b) { return a + b; };
cout << add(3, 4) << endl;   // 7

// Capture by value
int multiplier = 3;
auto times = [multiplier](int x) { return x * multiplier; };

// Capture by reference
int count = 0;
auto increment = [&count]() { count++; };

// Capture all by value [=], all by reference [&]
auto all_by_val = [=]() { /* can use any local var */ };
auto all_by_ref = [&]() { /* can modify any local var */ };

// Used with STL
vector<int> v = {3, 1, 4, 1, 5, 9};
sort(v.begin(), v.end(), [](int a, int b) { return a > b; }); // descending
```

### Function Pointers

```cpp
int add(int a, int b) { return a + b; }
int sub(int a, int b) { return a - b; }

// Function pointer
int (*op)(int, int) = add;
cout << op(3, 4) << endl;   // 7
op = sub;
cout << op(7, 3) << endl;   // 4

// Using typedef or using
using BinaryOp = int(*)(int, int);
BinaryOp func = add;
```

---

## 7. Arrays & Strings

### C-style Arrays

```cpp
int arr[5] = {1, 2, 3, 4, 5};
int zeros[10] = {};          // zero-initialized
int partial[5] = {1, 2};    // rest are zero

// Access
arr[0] = 10;

// Iterate
for (int i = 0; i < 5; i++) {
    cout << arr[i] << " ";
}

// 2D array
int matrix[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
cout << matrix[1][2] << endl;   // 6

// Passing array to function (decays to pointer)
void printArray(int* arr, int size) {
    for (int i = 0; i < size; i++) cout << arr[i] << " ";
}
```

### std::array (C++11)

```cpp
#include <array>

array<int, 5> arr = {1, 2, 3, 4, 5};
cout << arr.size() << endl;     // 5
cout << arr[0] << endl;
cout << arr.at(1) << endl;      // bounds-checked access
arr.fill(0);                    // fill all with 0
```

### std::vector

```cpp
#include <vector>

vector<int> v;                     // empty
vector<int> v2(5, 0);             // 5 elements, all 0
vector<int> v3 = {1, 2, 3, 4, 5};

v3.push_back(6);                  // append
v3.pop_back();                    // remove last
v3.insert(v3.begin() + 2, 99);   // insert at index 2
v3.erase(v3.begin() + 1);        // remove at index 1
v3.clear();                       // remove all

cout << v3.size() << endl;        // number of elements
cout << v3.capacity() << endl;    // allocated capacity
v3.reserve(100);                  // pre-allocate

// Access
v3[0];          // no bounds check
v3.at(0);       // bounds check (throws std::out_of_range)
v3.front();     // first element
v3.back();      // last element
```

### C-style Strings (char arrays)

```cpp
#include <cstring>

char name[] = "Alice";
char greeting[50] = "Hello";

strlen(name);            // 5 (excludes null terminator)
strcpy(greeting, name);  // copy name into greeting
strcat(greeting, "!");   // append
strcmp("abc", "abc");    // 0 if equal, <0 or >0 otherwise
```

### std::string (preferred)

```cpp
#include <string>

string s = "Hello, World!";
string s2("C++");
string s3(5, 'x');    // "xxxxx"

s.length();           // 13
s.size();             // same as length()
s.empty();            // false
s.clear();            // make empty

s + " " + s2;         // concatenation
s += "!";             // append
s.append(" more");    // append

s[0];                 // 'H' — no bounds check
s.at(0);              // 'H' — bounds check

s.substr(7, 5);       // "World" — start=7, length=5
s.find("World");      // returns position (string::npos if not found)
s.replace(0, 5, "Hi");

// Convert
stoi("42");           // string → int
stod("3.14");         // string → double
to_string(42);        // int → string

// Split (manual — no built-in split)
#include <sstream>
stringstream ss("one two three");
string word;
while (ss >> word) cout << word << endl;
```

---

## 8. Pointers & References

### Pointers

```cpp
int x = 10;
int* p = &x;         // p holds address of x

cout << p << endl;   // memory address
cout << *p << endl;  // 10 — dereference: value at address
*p = 20;             // modifies x through pointer
cout << x << endl;   // 20

// Null pointer
int* np = nullptr;   // C++11 (prefer over NULL or 0)
if (np == nullptr) cout << "null pointer" << endl;

// Pointer arithmetic
int arr[] = {10, 20, 30, 40, 50};
int* ptr = arr;
cout << *ptr << endl;      // 10
cout << *(ptr + 1) << endl; // 20 — moves by sizeof(int)
ptr++;
cout << *ptr << endl;      // 20

// Pointer to pointer
int** pp = &p;
cout << **pp << endl;      // 20
```

### Const and Pointers

```cpp
int x = 10;
const int* p1 = &x;     // pointer to const — can't modify *p1
int* const p2 = &x;     // const pointer — can't change where p2 points
const int* const p3 = &x; // both const
```

### References

```cpp
int x = 10;
int& ref = x;       // ref is an alias for x — MUST be initialized

ref = 20;           // x is now 20
cout << x << endl;  // 20

// References vs Pointers:
// - References cannot be null
// - References cannot be reassigned to refer to something else
// - No need to dereference
// - Syntax looks like regular variable usage
```

### Dynamic Memory (Raw — prefer smart pointers)

```cpp
// Allocate single value
int* p = new int(42);
cout << *p << endl;
delete p;           // MUST free or memory leak!
p = nullptr;        // good practice after delete

// Allocate array
int* arr = new int[10];
arr[0] = 1;
delete[] arr;       // use delete[] for arrays
arr = nullptr;
```

---

## 9. Object-Oriented Programming

### Classes & Objects

```cpp
class Dog {
private:                         // accessible only within class
    string name;
    int age;

public:                          // accessible from anywhere
    // Constructor
    Dog(string n, int a) : name(n), age(a) {}

    // Member functions (methods)
    void bark() const {
        cout << name << " says: Woof!" << endl;
    }

    // Getters (accessors)
    string getName() const { return name; }
    int getAge() const { return age; }

    // Setters (mutators)
    void setAge(int a) {
        if (a >= 0) age = a;
    }

    // Destructor
    ~Dog() {
        cout << name << " destroyed" << endl;
    }
};

// Create objects
Dog d1("Rex", 3);
Dog d2 = Dog("Buddy", 5);
Dog* d3 = new Dog("Luna", 2);

d1.bark();
cout << d1.getName() << endl;
d3->bark();      // arrow operator for pointer to object
delete d3;
```

### Constructors

```cpp
class Point {
public:
    double x, y;

    // Default constructor
    Point() : x(0), y(0) {}

    // Parameterized constructor
    Point(double x, double y) : x(x), y(y) {}

    // Copy constructor
    Point(const Point& other) : x(other.x), y(other.y) {}

    // Move constructor (C++11)
    Point(Point&& other) noexcept : x(other.x), y(other.y) {}

    // Delegating constructor (C++11)
    Point(double val) : Point(val, val) {}
};
```

### Static Members

```cpp
class Counter {
private:
    static int count;   // shared across all instances
public:
    Counter() { count++; }
    ~Counter() { count--; }
    static int getCount() { return count; }   // static method
};

int Counter::count = 0;   // definition outside class

Counter c1, c2, c3;
cout << Counter::getCount() << endl;   // 3
```

### Friend Functions & Classes

```cpp
class Box {
private:
    double width;
public:
    Box(double w) : width(w) {}
    friend double getWidth(const Box& b);   // friend function
    friend class BoxPrinter;                // friend class
};

double getWidth(const Box& b) {
    return b.width;   // can access private members
}
```

### Operator Overloading

```cpp
class Vector2D {
public:
    double x, y;
    Vector2D(double x, double y) : x(x), y(y) {}

    // + operator
    Vector2D operator+(const Vector2D& other) const {
        return Vector2D(x + other.x, y + other.y);
    }

    // == operator
    bool operator==(const Vector2D& other) const {
        return x == other.x && y == other.y;
    }

    // << operator (as friend for output)
    friend ostream& operator<<(ostream& os, const Vector2D& v) {
        os << "(" << v.x << ", " << v.y << ")";
        return os;
    }

    // [] operator
    double operator[](int i) const {
        return i == 0 ? x : y;
    }

    // prefix ++
    Vector2D& operator++() {
        x++; y++;
        return *this;
    }
};

Vector2D a(1, 2), b(3, 4);
Vector2D c = a + b;
cout << c << endl;   // (4, 6)
```

---

## 10. Inheritance & Polymorphism

### Inheritance

```cpp
// Base class
class Animal {
protected:
    string name;
    int age;
public:
    Animal(string n, int a) : name(n), age(a) {}

    void breathe() const {
        cout << name << " is breathing" << endl;
    }

    virtual void speak() const {   // virtual = can be overridden
        cout << name << " makes a sound" << endl;
    }

    virtual ~Animal() {}           // always virtual destructor in base class!
};

// Derived class — public inheritance
class Cat : public Animal {
public:
    Cat(string n, int a) : Animal(n, a) {}  // call base constructor

    void speak() const override {           // override keyword (C++11)
        cout << name << " says: Meow!" << endl;
    }

    void purr() const {
        cout << name << " purrs" << endl;
    }
};
```

### Access Specifiers in Inheritance

```cpp
class Base {
public:    int pub;
protected: int prot;
private:   int priv;
};

class PublicDerived    : public    Base {};  // pub→public, prot→protected
class ProtectedDerived : protected Base {};  // pub→protected, prot→protected
class PrivateDerived   : private   Base {};  // pub→private,  prot→private
// private is never inherited
```

### Virtual Functions & Polymorphism

```cpp
Animal* animals[3];
animals[0] = new Animal("Generic", 1);
animals[1] = new Cat("Whiskers", 3);
animals[2] = new Dog("Rex", 4);

for (int i = 0; i < 3; i++) {
    animals[i]->speak();   // calls correct version based on actual type!
}
// Output:
// Generic makes a sound
// Whiskers says: Meow!
// Rex says: Woof!

// Clean up
for (int i = 0; i < 3; i++) delete animals[i];
```

### Abstract Classes & Pure Virtual Functions

```cpp
class Shape {
public:
    virtual double area() const = 0;       // pure virtual — must override
    virtual double perimeter() const = 0;  // pure virtual

    void describe() const {
        cout << "Area: " << area() << endl;
    }

    virtual ~Shape() {}
};
// Cannot instantiate Shape directly!

class Circle : public Shape {
    double radius;
public:
    Circle(double r) : radius(r) {}
    double area() const override { return 3.14159 * radius * radius; }
    double perimeter() const override { return 2 * 3.14159 * radius; }
};

class Rectangle : public Shape {
    double w, h;
public:
    Rectangle(double w, double h) : w(w), h(h) {}
    double area() const override { return w * h; }
    double perimeter() const override { return 2 * (w + h); }
};
```

### Multiple Inheritance

```cpp
class Flyable {
public:
    virtual void fly() { cout << "Flying" << endl; }
};

class Swimmable {
public:
    virtual void swim() { cout << "Swimming" << endl; }
};

class Duck : public Flyable, public Swimmable {
    // Inherits both fly() and swim()
};

Duck d;
d.fly();
d.swim();
```

### Virtual Inheritance (diamond problem solution)

```cpp
class A { public: int val; };
class B : virtual public A {};
class C : virtual public A {};
class D : public B, public C {};  // only one copy of A::val
```

---

## 11. Templates

### Function Templates

```cpp
template <typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

cout << maximum(3, 7) << endl;       // 7 (int)
cout << maximum(3.5, 2.1) << endl;   // 3.5 (double)
cout << maximum('a', 'z') << endl;   // z (char)

// Multiple type parameters
template <typename T, typename U>
auto add(T a, U b) -> decltype(a + b) {
    return a + b;
}
```

### Class Templates

```cpp
template <typename T>
class Stack {
private:
    vector<T> data;
public:
    void push(const T& val) { data.push_back(val); }
    void pop() { data.pop_back(); }
    T top() const { return data.back(); }
    bool empty() const { return data.empty(); }
    int size() const { return data.size(); }
};

Stack<int> intStack;
intStack.push(10);
intStack.push(20);
cout << intStack.top() << endl;   // 20

Stack<string> strStack;
strStack.push("hello");
```

### Template Specialization

```cpp
// Primary template
template <typename T>
class TypeInfo {
public:
    static string name() { return "unknown"; }
};

// Full specialization for int
template <>
class TypeInfo<int> {
public:
    static string name() { return "int"; }
};

// Partial specialization for pointers
template <typename T>
class TypeInfo<T*> {
public:
    static string name() { return TypeInfo<T>::name() + "*"; }
};
```

### Variadic Templates (C++11)

```cpp
// Base case
void print() {}

// Recursive variadic template
template <typename T, typename... Args>
void print(T first, Args... rest) {
    cout << first << " ";
    print(rest...);
}

print(1, 2.5, "hello", 'c');   // 1 2.5 hello c
```

### Non-Type Template Parameters

```cpp
template <typename T, int N>
class Array {
    T data[N];
public:
    int size() const { return N; }
    T& operator[](int i) { return data[i]; }
};

Array<int, 5> arr;
arr[0] = 42;
cout << arr.size() << endl;   // 5
```

---

## 12. STL (Standard Template Library)

### Containers Overview

| Container | Header | Description |
|-----------|--------|-------------|
| `vector` | `<vector>` | Dynamic array |
| `deque` | `<deque>` | Double-ended queue |
| `list` | `<list>` | Doubly linked list |
| `forward_list` | `<forward_list>` | Singly linked list |
| `array` | `<array>` | Fixed-size array |
| `stack` | `<stack>` | LIFO stack (adaptor) |
| `queue` | `<queue>` | FIFO queue (adaptor) |
| `priority_queue` | `<queue>` | Heap-based priority queue |
| `set` | `<set>` | Sorted unique keys |
| `multiset` | `<set>` | Sorted non-unique keys |
| `map` | `<map>` | Sorted key-value pairs |
| `multimap` | `<map>` | Sorted non-unique key-value |
| `unordered_set` | `<unordered_set>` | Hash set |
| `unordered_map` | `<unordered_map>` | Hash map |

### map & unordered_map

```cpp
#include <map>
#include <unordered_map>

// map (sorted by key)
map<string, int> scores;
scores["Alice"] = 95;
scores["Bob"] = 87;
scores.insert({"Charlie", 92});

// Access
cout << scores["Alice"] << endl;
cout << scores.at("Bob") << endl;    // throws if not found

// Check existence
if (scores.count("Alice")) { /* exists */ }
if (scores.find("Alice") != scores.end()) { /* exists */ }

// Iterate
for (auto& [key, value] : scores) {    // C++17 structured binding
    cout << key << ": " << value << endl;
}

// unordered_map (O(1) average lookup, no sorting)
unordered_map<string, int> umap;
umap["x"] = 1;
umap["y"] = 2;
```

### set & unordered_set

```cpp
#include <set>

set<int> s = {5, 3, 1, 4, 2};   // automatically sorted: {1,2,3,4,5}
s.insert(6);
s.erase(3);
cout << s.count(1) << endl;      // 1 (exists) or 0 (doesn't)

for (int x : s) cout << x << " ";  // 1 2 4 5 6
```

### stack, queue, priority_queue

```cpp
#include <stack>
#include <queue>

// Stack (LIFO)
stack<int> st;
st.push(1); st.push(2); st.push(3);
cout << st.top() << endl;   // 3
st.pop();

// Queue (FIFO)
queue<int> q;
q.push(1); q.push(2); q.push(3);
cout << q.front() << endl;  // 1
q.pop();

// Priority Queue (max-heap by default)
priority_queue<int> pq;
pq.push(5); pq.push(1); pq.push(9);
cout << pq.top() << endl;   // 9 (largest first)

// Min-heap
priority_queue<int, vector<int>, greater<int>> minpq;
minpq.push(5); minpq.push(1); minpq.push(9);
cout << minpq.top() << endl;  // 1
```

### Iterators

```cpp
vector<int> v = {1, 2, 3, 4, 5};

// Iterator types
vector<int>::iterator it = v.begin();
auto it2 = v.begin();      // use auto

// Forward iteration
for (auto it = v.begin(); it != v.end(); ++it) {
    cout << *it << " ";
}

// Reverse iteration
for (auto it = v.rbegin(); it != v.rend(); ++it) {
    cout << *it << " ";
}

// Useful iterator functions
advance(it, 3);             // move forward 3 steps
distance(v.begin(), it);    // distance between iterators
next(it, 2);                // iterator 2 steps ahead (doesn't modify)
prev(it, 1);                // iterator 1 step back
```

### Algorithms (`<algorithm>`)

```cpp
#include <algorithm>
#include <numeric>

vector<int> v = {5, 2, 8, 1, 9, 3};

// Sorting
sort(v.begin(), v.end());                              // ascending
sort(v.begin(), v.end(), greater<int>());              // descending
sort(v.begin(), v.end(), [](int a, int b){ return a > b; }); // custom

// Searching
bool found = binary_search(v.begin(), v.end(), 5);    // requires sorted!
auto it = find(v.begin(), v.end(), 8);                 // linear search
auto it2 = lower_bound(v.begin(), v.end(), 5);         // first >= 5
auto it3 = upper_bound(v.begin(), v.end(), 5);         // first > 5

// Min/Max
int mn = *min_element(v.begin(), v.end());
int mx = *max_element(v.begin(), v.end());
auto [lo, hi] = minmax_element(v.begin(), v.end());

// Transform & Accumulate
transform(v.begin(), v.end(), v.begin(), [](int x){ return x * 2; });
int sum = accumulate(v.begin(), v.end(), 0);
int product = accumulate(v.begin(), v.end(), 1, multiplies<int>());

// Count & Remove
int cnt = count(v.begin(), v.end(), 5);
int cnt2 = count_if(v.begin(), v.end(), [](int x){ return x > 3; });
auto newEnd = remove(v.begin(), v.end(), 5);      // doesn't shrink!
v.erase(newEnd, v.end());                          // erase removed elements

// Fill & Generate
fill(v.begin(), v.end(), 0);
generate(v.begin(), v.end(), [n=0]() mutable { return n++; });

// Reverse & Rotate
reverse(v.begin(), v.end());
rotate(v.begin(), v.begin() + 2, v.end());

// Unique
sort(v.begin(), v.end());
auto last = unique(v.begin(), v.end());    // remove consecutive duplicates
v.erase(last, v.end());

// Copy & Move
vector<int> dest(v.size());
copy(v.begin(), v.end(), dest.begin());
copy_if(v.begin(), v.end(), back_inserter(dest), [](int x){ return x > 3; });
```

---

## 13. Memory Management

### Stack vs Heap

```
Stack:                        Heap:
- Automatic lifetime          - Manual lifetime (new/delete)
- Fast allocation             - Slower allocation
- Limited size                - Large, limited by RAM
- LIFO order                  - Random access
- Local variables             - Dynamic allocation
```

### Smart Pointers (C++11) — PREFER OVER RAW POINTERS

```cpp
#include <memory>

// unique_ptr — sole ownership, auto-deleted when out of scope
unique_ptr<int> up = make_unique<int>(42);
cout << *up << endl;
// No need to delete — automatic!

unique_ptr<int[]> arr = make_unique<int[]>(10);  // for arrays

// Transfer ownership with move
unique_ptr<int> up2 = move(up);    // up is now null
// up2 owns the resource now

// shared_ptr — shared ownership, reference counted
shared_ptr<int> sp1 = make_shared<int>(100);
shared_ptr<int> sp2 = sp1;          // both own it, ref count = 2
cout << sp1.use_count() << endl;    // 2
sp1.reset();                        // ref count = 1
// resource freed when last shared_ptr goes out of scope

// weak_ptr — non-owning reference (avoids circular references)
weak_ptr<int> wp = sp2;
if (auto locked = wp.lock()) {      // try to get shared_ptr
    cout << *locked << endl;
} else {
    cout << "Resource gone" << endl;
}
```

### RAII (Resource Acquisition Is Initialization)

```cpp
// RAII — tie resource lifetime to object lifetime
class FileHandle {
    FILE* file;
public:
    FileHandle(const char* name, const char* mode) {
        file = fopen(name, mode);
        if (!file) throw runtime_error("Cannot open file");
    }
    ~FileHandle() {
        if (file) fclose(file);   // always released
    }
    FILE* get() { return file; }
};

// File is automatically closed when fh goes out of scope
// Even if an exception is thrown!
{
    FileHandle fh("data.txt", "r");
    // use fh.get()
}  // fh destructor called here — file closed
```

### Memory Layout

```
High address  ┌──────────────┐
              │   Stack      │  ← grows downward
              │              │
              │     ↓        │
              │              │
              │     ↑        │
              │              │
              │   Heap       │  ← grows upward
              ├──────────────┤
              │   BSS        │  ← uninitialized globals
              ├──────────────┤
              │   Data       │  ← initialized globals/statics
              ├──────────────┤
Low address   │   Text/Code  │  ← program instructions
              └──────────────┘
```

---

## 14. Exception Handling

### try / catch / throw

```cpp
#include <stdexcept>

double divide(double a, double b) {
    if (b == 0) throw invalid_argument("Division by zero!");
    return a / b;
}

try {
    double result = divide(10, 0);
    cout << result << endl;
} catch (const invalid_argument& e) {
    cerr << "Invalid argument: " << e.what() << endl;
} catch (const runtime_error& e) {
    cerr << "Runtime error: " << e.what() << endl;
} catch (const exception& e) {
    cerr << "Exception: " << e.what() << endl;
} catch (...) {
    cerr << "Unknown exception" << endl;
}
```

### Standard Exception Hierarchy

```
std::exception
├── std::logic_error
│   ├── std::invalid_argument
│   ├── std::domain_error
│   ├── std::length_error
│   └── std::out_of_range
└── std::runtime_error
    ├── std::range_error
    ├── std::overflow_error
    └── std::underflow_error
```

### Custom Exceptions

```cpp
class NetworkError : public runtime_error {
    int errorCode;
public:
    NetworkError(const string& msg, int code)
        : runtime_error(msg), errorCode(code) {}
    int getCode() const { return errorCode; }
};

try {
    throw NetworkError("Connection refused", 503);
} catch (const NetworkError& e) {
    cerr << e.what() << " (code: " << e.getCode() << ")" << endl;
}
```

### noexcept

```cpp
void safeFunction() noexcept {    // guarantees no exceptions thrown
    // ...
}

// Move constructors/operators should be noexcept for optimization
MyClass(MyClass&& other) noexcept { /* ... */ }
```

---

## 15. File I/O

### Writing to a File

```cpp
#include <fstream>
#include <iostream>

// Write text to file
ofstream outFile("output.txt");
if (!outFile) {
    cerr << "Cannot open file!" << endl;
    return 1;
}
outFile << "Hello, File!" << endl;
outFile << "Line 2" << endl;
outFile.close();

// Append to file
ofstream appendFile("output.txt", ios::app);
appendFile << "Appended line" << endl;
```

### Reading from a File

```cpp
// Read line by line
ifstream inFile("input.txt");
if (!inFile) { cerr << "File not found!"; return 1; }

string line;
while (getline(inFile, line)) {
    cout << line << endl;
}
inFile.close();

// Read word by word
ifstream wordFile("input.txt");
string word;
while (wordFile >> word) {
    cout << word << " ";
}

// Read entire file into string
ifstream f("input.txt");
string content((istreambuf_iterator<char>(f)),
                istreambuf_iterator<char>());
```

### Binary File I/O

```cpp
struct Record {
    int id;
    double value;
    char name[50];
};

// Write binary
ofstream bin("data.bin", ios::binary);
Record r = {1, 3.14, "Alice"};
bin.write(reinterpret_cast<char*>(&r), sizeof(r));

// Read binary
ifstream binIn("data.bin", ios::binary);
Record r2;
binIn.read(reinterpret_cast<char*>(&r2), sizeof(r2));
cout << r2.id << " " << r2.value << " " << r2.name << endl;
```

### String Streams

```cpp
#include <sstream>

// ostringstream — build strings
ostringstream oss;
oss << "Value: " << 42 << ", Pi: " << 3.14;
string result = oss.str();

// istringstream — parse strings
string data = "10 20 30 40";
istringstream iss(data);
int n;
while (iss >> n) {
    cout << n * 2 << " ";
}
```

---

## 16. Modern C++ (C++11/14/17/20)

### auto & decltype

```cpp
auto x = 42;              // int
auto y = 3.14;            // double
auto z = "hello"s;        // std::string (with 's' suffix)

auto it = vec.begin();    // iterator type

decltype(x) a = x;        // same type as x
decltype(x + y) b = x;   // type of expression x+y
```

### Range-Based For & Structured Bindings (C++17)

```cpp
map<string, int> m = {{"a", 1}, {"b", 2}};
for (auto& [key, val] : m) {
    cout << key << "=" << val << endl;
}

auto [x, y, z] = make_tuple(1, 2.0, "three");
```

### Move Semantics & Rvalue References

```cpp
// lvalue = has a name/address
// rvalue = temporary, no persistent address

string s1 = "Hello";
string s2 = s1;              // copy — expensive for large objects
string s3 = move(s1);        // move — s1 is now empty, s3 owns data

// Rvalue reference
void process(string&& s) {   // only binds to rvalues/temporaries
    // can safely "steal" resources from s
}
process(string("temp"));     // OK — temporary is rvalue
// process(s2);              // ERROR — s2 is lvalue

// Perfect forwarding
template <typename T>
void wrapper(T&& arg) {
    process(forward<T>(arg));  // forward preserves lvalue/rvalue-ness
}
```

### std::optional (C++17)

```cpp
#include <optional>

optional<int> findUser(int id) {
    if (id == 42) return 42;
    return nullopt;   // no value
}

auto user = findUser(42);
if (user.has_value()) {
    cout << *user << endl;       // dereference
    cout << user.value() << endl;
}
cout << user.value_or(-1) << endl;  // default if empty
```

### std::variant (C++17)

```cpp
#include <variant>

variant<int, double, string> v;
v = 42;
v = 3.14;
v = "hello";

// Check and get
if (holds_alternative<string>(v)) {
    cout << get<string>(v) << endl;
}

// Visit
visit([](auto& val) { cout << val << endl; }, v);
```

### std::any (C++17)

```cpp
#include <any>

any a = 42;
a = 3.14;
a = string("hello");

cout << any_cast<string>(a) << endl;
```

### Concepts (C++20)

```cpp
#include <concepts>

// Define concept
template <typename T>
concept Numeric = is_arithmetic_v<T>;

// Use concept
template <Numeric T>
T add(T a, T b) { return a + b; }

// Abbreviated function template
auto multiply(Numeric auto a, Numeric auto b) {
    return a * b;
}
```

### Ranges (C++20)

```cpp
#include <ranges>
#include <algorithm>

vector<int> v = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

// Filter and transform with ranges
auto result = v
    | views::filter([](int x) { return x % 2 == 0; })   // even numbers
    | views::transform([](int x) { return x * x; });      // square them

for (int x : result) cout << x << " ";   // 4 16 36 64 100
```

### constexpr if (C++17)

```cpp
template <typename T>
void process(T value) {
    if constexpr (is_integral_v<T>) {
        cout << "Integer: " << value << endl;
    } else if constexpr (is_floating_point_v<T>) {
        cout << "Float: " << value << endl;
    } else {
        cout << "Other: " << value << endl;
    }
}
```

---

## 17. Concurrency & Multithreading

### std::thread (C++11)

```cpp
#include <thread>
#include <iostream>

void task(int id) {
    cout << "Thread " << id << " running" << endl;
}

int main() {
    thread t1(task, 1);
    thread t2(task, 2);

    t1.join();   // wait for t1 to finish
    t2.join();   // wait for t2 to finish

    // Detach (fire and forget — don't wait)
    thread t3(task, 3);
    t3.detach();

    return 0;
}
```

### Mutex & Lock

```cpp
#include <thread>
#include <mutex>

mutex mtx;
int counter = 0;

void increment() {
    for (int i = 0; i < 1000; i++) {
        lock_guard<mutex> lock(mtx);   // RAII lock — auto-released
        counter++;
    }
}

// unique_lock — more flexible
void task2() {
    unique_lock<mutex> lock(mtx);
    counter++;
    lock.unlock();   // manual unlock
    // ... do other stuff
    lock.lock();     // re-lock
}
```

### std::async & Futures

```cpp
#include <future>

int heavyComputation(int n) {
    // simulate work
    return n * n;
}

// Run asynchronously
future<int> f = async(launch::async, heavyComputation, 10);
// Do other work here...
int result = f.get();   // blocks until result is ready
cout << result << endl; // 100
```

### Atomic Variables

```cpp
#include <atomic>

atomic<int> atomicCounter = 0;

void safeIncrement() {
    for (int i = 0; i < 1000; i++) {
        atomicCounter++;   // thread-safe, no mutex needed
    }
}
```

### condition_variable

```cpp
#include <condition_variable>

mutex mtx;
condition_variable cv;
bool ready = false;

void worker() {
    unique_lock<mutex> lock(mtx);
    cv.wait(lock, []{ return ready; });   // wait until ready == true
    cout << "Worker running!" << endl;
}

void producer() {
    {
        lock_guard<mutex> lock(mtx);
        ready = true;
    }
    cv.notify_one();   // wake up one waiting thread
}
```

---

## 18. Best Practices & Common Mistakes

### Best Practices

```cpp
// 1. Prefer smart pointers over raw pointers
auto ptr = make_unique<MyClass>();   // NOT: MyClass* ptr = new MyClass();

// 2. Use const wherever possible
const string& getName() const;
void process(const vector<int>& v);

// 3. Use range-based for loops
for (const auto& item : container) { /* ... */ }

// 4. Prefer {} initialization (prevents narrowing)
int x{42};            // NOT: int x = 42.7; (silently truncates)

// 5. Use auto to reduce verbosity
auto it = myMap.find(key);   // NOT: map<string,int>::iterator it = ...

// 6. Always initialize variables
int x = 0;
string s = "";

// 7. Use override keyword
void myFunc() override;  // compiler error if base doesn't have virtual myFunc

// 8. Rule of 0/3/5
// Rule of 0: if you don't manage resources, don't write destructor/copy/move
// Rule of 3: if you define destructor, also define copy constructor + copy assignment
// Rule of 5: if you define any of 3, also define move constructor + move assignment

// 9. Use nullptr, not NULL or 0 for pointers
int* p = nullptr;

// 10. Prefer algorithms over raw loops
sort(v.begin(), v.end());         // NOT manual bubble sort
auto it = find(v.begin(), v.end(), val);

// 11. Pass large objects by const reference
void process(const BigObject& obj);  // NOT by value (expensive copy)

// 12. Return by value — compiler handles move/elision
BigObject createObject() {
    BigObject obj;
    return obj;   // NRVO/RVO optimizes this
}
```

### Common Mistakes

```cpp
// 1. Memory leak — forgetting delete
int* p = new int(5);
// ... forgot delete p!

// Fix: use smart pointers
auto p = make_unique<int>(5);

// 2. Dangling pointer — using pointer after delete
int* p = new int(5);
delete p;
cout << *p << endl;   // UNDEFINED BEHAVIOR!

// Fix: set to nullptr after delete
delete p; p = nullptr;

// 3. Array out of bounds
int arr[5];
arr[5] = 10;   // UNDEFINED BEHAVIOR — valid indices are 0-4

// 4. Integer overflow
int x = INT_MAX;
x++;   // overflow — undefined behavior for signed int

// 5. Forgetting virtual destructor
class Base {
public:
    ~Base() {}   // NOT virtual — derived destructor won't be called!
};
// Fix:
    virtual ~Base() {}

// 6. Object slicing
Derived d;
Base b = d;   // slices off derived part — only Base data remains

// Fix: use pointers/references for polymorphism
Base& bref = d;

// 7. Modifying container while iterating
for (auto it = v.begin(); it != v.end(); ++it) {
    if (*it == 3) v.erase(it);   // it is now invalid!
}
// Fix:
it = v.erase(it);   // erase returns valid next iterator

// 8. Race condition — unsynchronized shared data
int counter = 0;  // accessed by multiple threads without mutex — undefined behavior

// 9. Comparing floats with ==
if (0.1 + 0.2 == 0.3)   // FALSE due to floating point precision!
// Fix:
if (abs(0.1 + 0.2 - 0.3) < 1e-9)

// 10. Infinite recursion / missing base case
int bad(int n) {
    return n + bad(n - 1);   // no base case — stack overflow!
}
```

### Useful Compiler Flags

```bash
# Debug build
g++ -std=c++17 -g -O0 -Wall -Wextra -Wpedantic -o prog main.cpp

# Release build
g++ -std=c++17 -O2 -DNDEBUG -o prog main.cpp

# Address sanitizer (detects memory errors)
g++ -fsanitize=address -g main.cpp

# Thread sanitizer (detects race conditions)
g++ -fsanitize=thread -g main.cpp

# Undefined behavior sanitizer
g++ -fsanitize=undefined -g main.cpp
```

---

## Quick Reference Cheat Sheet

### Container Time Complexities

| Operation | vector | deque | list | set/map | unordered |
|-----------|--------|-------|------|---------|-----------|
| Access by index | O(1) | O(1) | O(n) | — | — |
| Insert at end | O(1) amort | O(1) | O(1) | O(log n) | O(1) avg |
| Insert at front | O(n) | O(1) | O(1) | O(log n) | O(1) avg |
| Insert middle | O(n) | O(n) | O(1) | O(log n) | O(1) avg |
| Search | O(n) | O(n) | O(n) | O(log n) | O(1) avg |
| Delete | O(n) | O(n) | O(1) | O(log n) | O(1) avg |

### Common Headers

```cpp
#include <iostream>      // cin, cout, cerr
#include <string>        // std::string
#include <vector>        // std::vector
#include <array>         // std::array
#include <map>           // std::map, std::multimap
#include <unordered_map> // std::unordered_map
#include <set>           // std::set, std::multiset
#include <unordered_set> // std::unordered_set
#include <stack>         // std::stack
#include <queue>         // std::queue, std::priority_queue
#include <algorithm>     // sort, find, transform, etc.
#include <numeric>       // accumulate, iota, etc.
#include <functional>    // greater, less, bind, function
#include <memory>        // unique_ptr, shared_ptr, make_unique
#include <utility>       // pair, make_pair, move, forward
#include <tuple>         // tuple, make_tuple, get
#include <optional>      // optional (C++17)
#include <variant>       // variant (C++17)
#include <any>           // any (C++17)
#include <fstream>       // file I/O
#include <sstream>       // string streams
#include <thread>        // std::thread
#include <mutex>         // std::mutex, lock_guard
#include <future>        // std::async, std::future
#include <atomic>        // std::atomic
#include <chrono>        // time utilities
#include <random>        // random number generation
#include <cmath>         // math functions (sqrt, pow, sin, etc.)
#include <cstring>       // C-style string functions
#include <cstdint>       // fixed-width integer types
#include <limits>        // numeric_limits
#include <stdexcept>     // standard exceptions
#include <cassert>       // assert()
#include <ranges>        // ranges (C++20)
#include <concepts>      // concepts (C++20)
```

---

*Generated as a complete C++ reference guide. Use alongside a compiler — the best way to learn is by writing and running code.*
