# C++ Complete Guide — Beginner to Advanced

> Don't panic. This guide starts from absolute zero and builds up step by step.
> Every concept has a simple English explanation + code. Read it like a story.

---

## Table of Contents

### 🟢 Beginner
1. [What is C++?](#1-what-is-c)
2. [Your First Program](#2-your-first-program)
3. [Variables & Data Types](#3-variables--data-types)
4. [Getting Input from User](#4-getting-input-from-user)
5. [Operators](#5-operators)
6. [Making Decisions (if/else)](#6-making-decisions-ifelse)
7. [Loops](#7-loops)
8. [Functions](#8-functions)
9. [Arrays](#9-arrays)
10. [Strings](#10-strings)

### 🟡 Intermediate
11. [Pointers & References](#11-pointers--references)
12. [Object-Oriented Programming](#12-object-oriented-programming-oop)
13. [Inheritance & Polymorphism](#13-inheritance--polymorphism)
14. [File Input & Output](#14-file-input--output)
15. [Error Handling (Exceptions)](#15-error-handling-exceptions)
16. [The STL — Standard Template Library](#16-the-stl--standard-template-library)

### 🔴 Advanced
17. [Templates](#17-templates)
18. [Smart Pointers & Memory Management](#18-smart-pointers--memory-management)
19. [Modern C++ (C++11 to C++20)](#19-modern-c-c11-to-c20)
20. [Multithreading](#20-multithreading)
21. [Best Practices & Common Mistakes](#21-best-practices--common-mistakes)
22. [Quick Reference Cheat Sheet](#22-quick-reference-cheat-sheet)

---

# 🟢 BEGINNER

---

## 1. What is C++?

**In simple words:** C++ is a programming language that lets you talk to a computer and tell it what to do. It is one of the fastest languages ever made.

**Where is C++ used?**
- Games — Unreal Engine, most AAA games (GTA, Fortnite engine)
- Operating Systems — Windows, Linux parts
- Browsers — Chrome, Firefox internals
- Databases — MySQL, MongoDB
- Embedded systems — cars, robots, IoT devices

**C++ vs other languages:**

| Language | Speed | Difficulty | Used For |
|----------|-------|------------|----------|
| C++ | Fastest | Hard | Games, OS, performance apps |
| Python | Slow | Easy | AI, scripting, data science |
| Java | Medium | Medium | Android, enterprise, Minecraft |
| JavaScript | Medium | Easy | Web |

**How C++ works:**
```
You write code  →  Compiler translates to machine code  →  Computer runs it
  (main.cpp)           (g++ compiler)                      (very fast!)
```

**Installing a compiler:**
```bash
# Windows: Download MinGW from mingw-w64.org, or install Visual Studio

# Mac:
xcode-select --install

# Linux (Ubuntu/Debian):
sudo apt install g++

# Check if installed:
g++ --version
```

---

## 2. Your First Program

```cpp
#include <iostream>    // loads the tools for printing text

int main() {           // every C++ program starts from main()
    std::cout << "Hello, World!" << std::endl;
    return 0;          // 0 = program finished successfully
}
```

**Line by line:**

| Line | What it means |
|------|---------------|
| `#include <iostream>` | Import the input/output library (like a toolbox) |
| `int main()` | This is where your program starts |
| `std::cout <<` | Print to the screen |
| `std::endl` | Go to next line (like pressing Enter) |
| `return 0;` | Tell the OS: no errors, done |

**Compile and run:**
```bash
g++ hello.cpp -o hello    # compile: creates the program
./hello                    # run on Linux/Mac
hello.exe                  # run on Windows
```

**Avoid typing `std::` everywhere:**
```cpp
#include <iostream>
using namespace std;   // now write cout instead of std::cout

int main() {
    cout << "Hello!" << endl;
    return 0;
}
```

**Printing multiple things:**
```cpp
cout << "My name is " << "Alice" << endl;
cout << "I am " << 20 << " years old" << endl;
cout << "Pi is " << 3.14159 << endl;
cout << "Two plus two is " << 2 + 2 << endl;
```

**Comments:**
```cpp
// This is a single line comment — ignored by compiler

/* This is a
   multi-line comment */

int x = 5;  // inline comment after code
```

---

## 3. Variables & Data Types

**What is a variable?**
A variable is a named box that stores a value. You give it a type and a name.

```
int age = 25;
 ↑    ↑    ↑
type  name  value
```

### The Basic Types

```cpp
// Whole numbers (integers)
int age = 25;                  // standard integer: -2 billion to +2 billion
long long bigNum = 9999999999; // very large integer
short small = 100;             // small integer (saves memory)

// Decimal numbers
float price = 9.99f;           // 7 digits of precision — add 'f' at end
double pi = 3.14159265358;     // 15 digits of precision — prefer this

// Single character
char grade = 'A';              // single quotes for char!
char letter = 'z';

// True or False
bool isRaining = false;
bool isSunny = true;

// Text
string name = "Alice";         // needs #include <string>
string message = "Hello World";
```

### Variable Rules
```cpp
// Valid names
int myAge = 20;
int player1Score = 0;
int _counter = 0;
int totalAmount = 100;

// Invalid names — these cause errors
int 1player = 0;    // cannot start with a number
int my age = 0;     // cannot have spaces
int int = 0;        // cannot use reserved words like int, for, while

// Case sensitive — these are THREE different variables
int score = 10;
int Score = 20;
int SCORE = 30;
```

### Constants — values that never change
```cpp
const double PI = 3.14159265;
const int MAX_PLAYERS = 4;
const string GAME_NAME = "Pong";

PI = 3;   // ERROR: cannot change a constant
```

### Checking type sizes
```cpp
cout << sizeof(int)    << " bytes" << endl;  // 4
cout << sizeof(double) << " bytes" << endl;  // 8
cout << sizeof(char)   << " bytes" << endl;  // 1
cout << sizeof(bool)   << " bytes" << endl;  // 1
```

### Type conversion
```cpp
int x = 10;
double y = x;              // int to double: safe, automatic

double d = 9.99;
int i = d;                 // double to int: loses the .99 silently — careful!
int i2 = static_cast<int>(d);  // same result, but explicit = better practice

// Examples
int a = 7, b = 2;
double result = a / b;           // result = 3.0  (integer division first!)
double result2 = (double)a / b;  // result2 = 3.5 (cast a first, then divide)
```

---

## 4. Getting Input from User

```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    cout << "Enter your age: ";
    cin >> age;    // cin reads from keyboard, >> puts it in the variable
    cout << "You are " << age << " years old!" << endl;
    return 0;
}
```

**Reading multiple values:**
```cpp
int a, b;
cout << "Enter two numbers separated by space: ";
cin >> a >> b;
cout << "Sum = " << a + b << endl;
```

**Reading a full sentence (with spaces):**
```cpp
string fullName;
cout << "Enter your full name: ";
getline(cin, fullName);   // reads entire line including spaces
cout << "Hello, " << fullName << "!" << endl;
```

**Important: mixing cin and getline:**
```cpp
int age;
cin >> age;
cin.ignore();              // clears the leftover newline — REQUIRED before getline
string name;
getline(cin, name);        // now works correctly
```

---

## 5. Operators

### Math Operators
```cpp
int a = 10, b = 3;

cout << a + b << endl;   // 13 — addition
cout << a - b << endl;   // 7  — subtraction
cout << a * b << endl;   // 30 — multiplication
cout << a / b << endl;   // 3  — integer division (no decimals!)
cout << a % b << endl;   // 1  — remainder (10 = 3*3 + 1)

// To get decimal division, use doubles
double x = 10.0, y = 3.0;
cout << x / y << endl;   // 3.333...

// Shortcuts
a += 5;   // a = a + 5  → a is now 15
a -= 2;   // a = a - 2  → a is now 13
a *= 2;   // a = a * 2  → a is now 26
a /= 2;   // a = a / 2  → a is now 13
a %= 4;   // a = a % 4  → a is now 1

// Increment and Decrement
int n = 5;
n++;      // n becomes 6 (post-increment: use value THEN add 1)
++n;      // n becomes 7 (pre-increment: add 1 THEN use value)
n--;      // n becomes 6
```

### Comparison Operators (result is true or false)
```cpp
int x = 5, y = 10;
cout << (x == y) << endl;  // 0 = false — are they equal?
cout << (x != y) << endl;  // 1 = true  — are they different?
cout << (x < y)  << endl;  // 1 = true  — less than?
cout << (x > y)  << endl;  // 0 = false — greater than?
cout << (x <= 5) << endl;  // 1 = true  — less than or equal?
cout << (x >= 5) << endl;  // 1 = true  — greater than or equal?
```

### Logical Operators
```cpp
// && = AND: both conditions must be true
// || = OR:  at least one must be true
// !  = NOT: flips true to false and vice versa

int age = 25;
bool hasTicket = true;

if (age >= 18 && hasTicket) {
    cout << "You can enter!" << endl;
}

bool isWeekend = true;
bool isHoliday = false;
if (isWeekend || isHoliday) {
    cout << "No school today!" << endl;
}

bool isLoggedIn = false;
if (!isLoggedIn) {
    cout << "Please log in first" << endl;
}
```

---

## 6. Making Decisions (if/else)

### Basic if / else if / else
```cpp
int score = 75;

if (score >= 90) {
    cout << "Grade A — Excellent!" << endl;
} else if (score >= 80) {
    cout << "Grade B — Good" << endl;
} else if (score >= 70) {
    cout << "Grade C — Average" << endl;
} else if (score >= 60) {
    cout << "Grade D — Below average" << endl;
} else {
    cout << "Grade F — Failed" << endl;
}
```

### switch — cleaner for exact value matching
```cpp
int day = 3;

switch (day) {
    case 1:
        cout << "Monday" << endl;
        break;    // IMPORTANT: without break it falls into next case
    case 2:
        cout << "Tuesday" << endl;
        break;
    case 3:
        cout << "Wednesday" << endl;
        break;
    case 4:
        cout << "Thursday" << endl;
        break;
    case 5:
        cout << "Friday" << endl;
        break;
    case 6:
    case 7:
        cout << "Weekend!" << endl;   // cases 6 and 7 share this
        break;
    default:
        cout << "Invalid day" << endl;
}
```

### Ternary — one-line if/else
```cpp
int age = 20;
string label = (age >= 18) ? "adult" : "minor";
// If age >= 18 → "adult", otherwise → "minor"
cout << label << endl;   // adult

int a = 5, b = 9;
int bigger = (a > b) ? a : b;
cout << bigger << endl;  // 9
```

---

## 7. Loops

### while — repeat while condition is true
```cpp
int i = 1;
while (i <= 5) {
    cout << i << " ";
    i++;
}
// Output: 1 2 3 4 5

// Countdown example
int count = 10;
while (count > 0) {
    cout << count << "... ";
    count--;
}
cout << "Blast off!" << endl;
```

### do-while — always runs at least once
```cpp
int number;
do {
    cout << "Enter a positive number: ";
    cin >> number;
} while (number <= 0);   // if negative, ask again
cout << "You entered: " << number << endl;
```

### for — best when you know how many times
```cpp
// for (start; condition; step)
for (int i = 0; i < 5; i++) {
    cout << i << " ";
}
// Output: 0 1 2 3 4

// Count from 1 to 10
for (int i = 1; i <= 10; i++) {
    cout << i << " ";
}

// Count backwards
for (int i = 10; i >= 1; i--) {
    cout << i << " ";
}

// Every other number
for (int i = 0; i <= 20; i += 2) {
    cout << i << " ";
}
// Output: 0 2 4 6 8 10 12 14 16 18 20
```

### break and continue
```cpp
// break: exit the loop completely
for (int i = 0; i < 100; i++) {
    if (i == 5) break;
    cout << i << " ";
}
// Output: 0 1 2 3 4

// continue: skip this iteration, go to next
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) continue;   // skip even numbers
    cout << i << " ";
}
// Output: 1 3 5 7 9
```

### Nested loops (loop inside a loop)
```cpp
// Print multiplication table
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= 5; j++) {
        cout << i * j << "\t";   // \t = tab for alignment
    }
    cout << endl;
}

// Print a triangle pattern
for (int i = 1; i <= 5; i++) {
    for (int j = 0; j < i; j++) {
        cout << "* ";
    }
    cout << endl;
}
// Output:
// *
// * *
// * * *
// * * * *
// * * * * *
```

---

## 8. Functions

**What is a function?**
A named block of code you can run (call) whenever you want. Instead of writing the same logic 10 times, write it once as a function.

```cpp
// Structure:
// returnType functionName(parameter1Type param1, ...) {
//     body
//     return value;
// }

int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(3, 4);      // call the function
    cout << result << endl;      // 7

    cout << add(10, 20) << endl; // 30
    cout << add(100, 200) << endl; // 300
    return 0;
}
```

### void — functions that don't return a value
```cpp
void printLine() {
    cout << "-------------------" << endl;
}

void greet(string name) {
    cout << "Hello, " << name << "!" << endl;
}

printLine();
greet("Alice");
greet("Bob");
printLine();
```

### Default parameters
```cpp
// Parameters with defaults must be at the END
void introduce(string name, int age = 18, string city = "Unknown") {
    cout << name << ", age " << age << ", from " << city << endl;
}

introduce("Alice", 25, "New York");   // Alice, age 25, from New York
introduce("Bob", 30);                 // Bob, age 30, from Unknown
introduce("Charlie");                 // Charlie, age 18, from Unknown
```

### Function overloading — same name, different parameters
```cpp
void print(int x) {
    cout << "Integer: " << x << endl;
}
void print(double x) {
    cout << "Double: " << x << endl;
}
void print(string x) {
    cout << "String: " << x << endl;
}

print(42);       // Integer: 42
print(3.14);     // Double: 3.14
print("hello");  // String: hello
```

### Pass by reference — modify the original variable
```cpp
// By value: function gets a COPY, original unchanged
void byValue(int x) {
    x = 100;   // only changes the local copy
}

// By reference: function works with the ORIGINAL
void byReference(int& x) {   // & means reference
    x = 100;   // changes the original variable
}

int num = 5;
byValue(num);
cout << num << endl;     // still 5

byReference(num);
cout << num << endl;     // now 100!

// Common use: swap two variables
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}
```

### Recursion — function that calls itself
```cpp
// factorial(5) = 5 * 4 * 3 * 2 * 1 = 120
int factorial(int n) {
    if (n == 0 || n == 1) return 1;   // BASE CASE: stop here
    return n * factorial(n - 1);       // recursive call with smaller n
}

cout << factorial(5)  << endl;  // 120
cout << factorial(10) << endl;  // 3628800

// Fibonacci: 0 1 1 2 3 5 8 13 21...
int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

### Function declaration vs definition
```cpp
// If function is defined AFTER main, declare it first at the top
int multiply(int a, int b);   // declaration (prototype) — just the signature

int main() {
    cout << multiply(3, 4) << endl;   // can use it before definition
    return 0;
}

int multiply(int a, int b) {   // definition — the actual implementation
    return a * b;
}
```

---

## 9. Arrays

**What is an array?**
A container that holds multiple values of the SAME type. Like a row of numbered boxes.

```
Index:   [0]  [1]  [2]  [3]  [4]
         ┌────┬────┬────┬────┬────┐
Values:  │ 90 │ 85 │ 78 │ 92 │ 88 │
         └────┴────┴────┴────┴────┘
Note: Index always starts at 0!
```

```cpp
// Declare and initialize
int scores[5] = {90, 85, 78, 92, 88};

// Access elements
cout << scores[0] << endl;   // 90 (first)
cout << scores[4] << endl;   // 88 (last)

// Modify
scores[2] = 100;

// Get size (in number of elements)
int size = sizeof(scores) / sizeof(scores[0]);  // 5

// Loop through
for (int i = 0; i < 5; i++) {
    cout << "Score " << i << ": " << scores[i] << endl;
}
```

### Important: array bounds!
```cpp
int arr[3] = {10, 20, 30};
cout << arr[0] << endl;   // 10 — valid
cout << arr[2] << endl;   // 30 — valid (last)
cout << arr[3] << endl;   // DANGER! Index 3 doesn't exist → undefined behavior
```

### 2D Arrays — like a grid or table
```cpp
int matrix[3][4] = {       // 3 rows, 4 columns
    {1,  2,  3,  4},
    {5,  6,  7,  8},
    {9, 10, 11, 12}
};

cout << matrix[0][0] << endl;   // 1  (row 0, col 0)
cout << matrix[1][2] << endl;   // 7  (row 1, col 2)
cout << matrix[2][3] << endl;   // 12 (row 2, col 3)

// Print all
for (int row = 0; row < 3; row++) {
    for (int col = 0; col < 4; col++) {
        cout << matrix[row][col] << " ";
    }
    cout << endl;
}
```

### Vectors — better arrays (flexible size)
```cpp
#include <vector>

vector<int> v = {1, 2, 3};

v.push_back(4);     // add to end: {1,2,3,4}
v.push_back(5);     // {1,2,3,4,5}
v.pop_back();       // remove last: {1,2,3,4}

cout << v.size() << endl;   // 4
cout << v[0]     << endl;   // 1

// Range-based loop
for (int x : v) {
    cout << x << " ";
}

// Initialize with N copies
vector<int> zeros(10, 0);    // 10 zeros: {0,0,0,0,0,0,0,0,0,0}
vector<string> names(3, "unknown");  // {"unknown","unknown","unknown"}
```

---

## 10. Strings

```cpp
#include <string>
using namespace std;

string s = "Hello, World!";

// Length
cout << s.length() << endl;         // 13
cout << s.size() << endl;           // same as length()

// Access single character
cout << s[0] << endl;               // H
cout << s[7] << endl;               // W

// Concatenation (joining strings)
string first = "Hello";
string second = "World";
string combined = first + " " + second;   // "Hello World"
first += "!";                             // first is now "Hello!"

// Substring: extract part of string
// s.substr(startIndex, length)
cout << s.substr(7, 5) << endl;     // World

// Find
int pos = s.find("World");
cout << pos << endl;                // 7

// Check if something exists
if (s.find("Hello") != string::npos) {
    cout << "Found Hello!" << endl;
}

// Replace
s.replace(0, 5, "Hi");             // "Hi, World!"

// Compare
if (first == second) cout << "same" << endl;
else cout << "different" << endl;

// Convert
string numStr = to_string(42);      // int → string: "42"
int num = stoi("123");              // string → int: 123
double d = stod("3.14");           // string → double: 3.14

// Empty check
string empty = "";
if (empty.empty()) cout << "String is empty" << endl;
```

---

# 🟡 INTERMEDIATE

---

## 11. Pointers & References

### What is a pointer?
A pointer stores a **memory address** — it tells you WHERE a variable lives in memory.

Think of it like this: your variable is a house, the pointer is the house's address written on a piece of paper.

```cpp
int age = 25;

cout << age  << endl;    // 25          — the actual value
cout << &age << endl;    // 0x7ffd...   — the memory address (& = "address of")

int* ptr = &age;         // ptr stores the address of age
//   ↑ * means "pointer to int"

cout << ptr  << endl;    // same address as &age
cout << *ptr << endl;    // 25 — dereference: get the value at that address
//          ↑ * here means "value at this address"
```

### Modifying through a pointer
```cpp
int x = 10;
int* p = &x;

cout << x    << endl;   // 10
*p = 99;                // change value at the address
cout << x    << endl;   // 99 — x changed because p points to x
```

### References — simpler aliasing
```cpp
int x = 10;
int& ref = x;   // ref is another name for x (must initialize immediately)

ref = 20;
cout << x << endl;    // 20 — same variable, different name

// Great for function parameters
void doubleValue(int& n) {
    n *= 2;    // modifies original
}
int num = 5;
doubleValue(num);
cout << num << endl;   // 10
```

### Pointer vs Reference

| Feature | Pointer | Reference |
|---------|---------|-----------|
| Can be null | Yes (`nullptr`) | No — always valid |
| Can change target | Yes | No — fixed to one variable |
| Syntax to use value | `*ptr` (dereference) | Just use `ref` directly |
| Typical use | Dynamic memory, arrays | Function parameters |

### nullptr — safe empty pointer
```cpp
int* p = nullptr;   // points to nothing

if (p == nullptr) {
    cout << "Pointer is empty — don't dereference!" << endl;
}

// Never dereference a nullptr or dangling pointer!
// *p = 5;   // CRASH — writing to address 0
```

---

## 12. Object-Oriented Programming (OOP)

**What is OOP?**
Instead of just writing instructions, you model your program as a collection of **objects** — things that have both data (what they are) and behavior (what they do).

Real world: A Dog has a name, breed, age. It can bark, eat, sleep.
In C++: A `Dog` class has those properties and methods.

### Class — the blueprint
```cpp
#include <iostream>
#include <string>
using namespace std;

class Dog {
public:
    // Data (properties/attributes)
    string name;
    string breed;
    int age;

    // Behavior (methods/functions)
    void bark() {
        cout << name << " says: Woof!" << endl;
    }

    void introduce() {
        cout << "I'm " << name << ", a " << breed
             << ", " << age << " years old." << endl;
    }
};

int main() {
    Dog d1;                  // create object from class blueprint
    d1.name  = "Rex";
    d1.breed = "Husky";
    d1.age   = 3;
    d1.bark();               // Rex says: Woof!
    d1.introduce();

    Dog d2;
    d2.name  = "Buddy";
    d2.breed = "Labrador";
    d2.age   = 5;
    d2.bark();               // Buddy says: Woof!
    return 0;
}
```

### Constructor — runs automatically when object is created
```cpp
class Car {
public:
    string brand;
    string color;
    int speed;

    // Constructor — same name as class, no return type
    Car(string b, string c) {
        brand = b;
        color = c;
        speed = 0;
    }

    // Cleaner style using initializer list
    Car(string b, string c) : brand(b), color(c), speed(0) {}

    void accelerate(int amount) {
        speed += amount;
        cout << brand << " is now going " << speed << " km/h" << endl;
    }

    void info() {
        cout << color << " " << brand << " at " << speed << " km/h" << endl;
    }
};

Car c1("Toyota", "Red");   // constructor called automatically
Car c2("BMW", "Blue");
c1.accelerate(50);
c2.accelerate(100);
c1.info();
```

### Encapsulation — private vs public
```cpp
class BankAccount {
private:                      // only accessible INSIDE this class
    string owner;
    double balance;

public:                       // accessible from ANYWHERE
    // Constructor
    BankAccount(string name, double initialBalance) {
        owner = name;
        balance = (initialBalance >= 0) ? initialBalance : 0;
    }

    // Getter — read-only access to private data
    double getBalance() const {
        return balance;
    }

    string getOwner() const {
        return owner;
    }

    // Methods that control how balance changes
    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            cout << "Deposited $" << amount << endl;
        }
    }

    void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            cout << "Withdrew $" << amount << endl;
        } else {
            cout << "Insufficient funds or invalid amount" << endl;
        }
    }

    void printStatement() const {
        cout << owner << "'s balance: $" << balance << endl;
    }
};

BankAccount acc("Alice", 1000);
acc.deposit(500);       // Deposited $500
acc.withdraw(200);      // Withdrew $200
acc.printStatement();   // Alice's balance: $1300
// acc.balance = 999999; // ERROR — balance is private!
```

### Destructor — cleanup when object is destroyed
```cpp
class FileManager {
public:
    string filename;

    FileManager(string fn) : filename(fn) {
        cout << "Opening " << filename << endl;
    }

    ~FileManager() {   // destructor — tilde prefix, no params, no return
        cout << "Closing " << filename << endl;
    }
};

int main() {
    {
        FileManager fm("data.txt");   // "Opening data.txt"
        // use fm...
    }  // fm goes out of scope here — "Closing data.txt" printed automatically
    return 0;
}
```

### Operator Overloading — make operators work with your types
```cpp
class Vector2 {
public:
    double x, y;

    Vector2(double x, double y) : x(x), y(y) {}

    // Overload + operator
    Vector2 operator+(const Vector2& other) const {
        return Vector2(x + other.x, y + other.y);
    }

    // Overload == operator
    bool operator==(const Vector2& other) const {
        return x == other.x && y == other.y;
    }

    // Overload << for printing
    friend ostream& operator<<(ostream& os, const Vector2& v) {
        os << "(" << v.x << ", " << v.y << ")";
        return os;
    }
};

Vector2 a(1, 2), b(3, 4);
Vector2 c = a + b;
cout << c << endl;   // (4, 6)
```

---

## 13. Inheritance & Polymorphism

**Inheritance:** A child class gets everything from the parent, then adds its own stuff.

```
Animal
├── Dog  (has everything Animal has + dog-specific things)
├── Cat  (has everything Animal has + cat-specific things)
└── Bird (has everything Animal has + bird-specific things)
```

```cpp
// Parent (Base) class
class Animal {
protected:                  // accessible in child classes but not outside
    string name;
    int age;

public:
    Animal(string n, int a) : name(n), age(a) {}

    void breathe() {
        cout << name << " is breathing" << endl;
    }

    // virtual = child classes CAN override this
    virtual void speak() {
        cout << name << " makes a sound" << endl;
    }

    string getName() { return name; }

    virtual ~Animal() {}    // ALWAYS make destructor virtual in base class!
};

// Child (Derived) class
class Dog : public Animal {
    string breed;
public:
    Dog(string n, int a, string b) : Animal(n, a), breed(b) {}

    void speak() override {     // override keyword: compiler checks if parent has this
        cout << name << " barks: Woof!" << endl;
    }

    void fetch() {
        cout << name << " fetches the ball!" << endl;
    }
};

class Cat : public Animal {
public:
    Cat(string n, int a) : Animal(n, a) {}

    void speak() override {
        cout << name << " meows: Meow!" << endl;
    }

    void purr() {
        cout << name << " is purring..." << endl;
    }
};

int main() {
    Dog d("Rex", 3, "Husky");
    Cat c("Luna", 2);

    d.breathe();   // inherited from Animal
    d.speak();     // Dog's version
    d.fetch();     // Dog only

    c.breathe();   // inherited from Animal
    c.speak();     // Cat's version
    c.purr();      // Cat only

    return 0;
}
```

### Polymorphism — one pointer, many types
```cpp
// The real power of virtual functions
Animal* animals[3];
animals[0] = new Animal("Generic", 1);
animals[1] = new Dog("Rex", 3, "Husky");
animals[2] = new Cat("Luna", 2);

for (int i = 0; i < 3; i++) {
    animals[i]->speak();   // calls correct version based on ACTUAL type
}
// Output:
// Generic makes a sound
// Rex barks: Woof!
// Luna meows: Meow!

for (int i = 0; i < 3; i++) delete animals[i];
```

### Abstract class — force child to implement methods
```cpp
class Shape {
public:
    // pure virtual = must be implemented by child (= 0 syntax)
    virtual double area() = 0;
    virtual double perimeter() = 0;
    virtual string name() = 0;

    // Shape cannot be instantiated — it's just a contract
    void print() {
        cout << name() << ": area=" << area()
             << ", perimeter=" << perimeter() << endl;
    }
    virtual ~Shape() {}
};

class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    double area() override { return 3.14159 * r * r; }
    double perimeter() override { return 2 * 3.14159 * r; }
    string name() override { return "Circle(r=" + to_string(r) + ")"; }
};

class Rectangle : public Shape {
    double w, h;
public:
    Rectangle(double w, double h) : w(w), h(h) {}
    double area() override { return w * h; }
    double perimeter() override { return 2*(w+h); }
    string name() override { return "Rect(" + to_string(w) + "x" + to_string(h) + ")"; }
};

Circle c(5);
Rectangle r(4, 6);
c.print();   // Circle(r=5): area=78.539..., perimeter=31.415...
r.print();   // Rect(4x6): area=24, perimeter=20
```

---

## 14. File Input & Output

```cpp
#include <fstream>
#include <string>
using namespace std;
```

### Writing to a file
```cpp
ofstream file("notes.txt");   // creates/overwrites the file

if (!file.is_open()) {
    cout << "Could not open file!" << endl;
    return 1;
}

file << "Line 1: Hello" << endl;
file << "Line 2: World" << endl;
file << "Number: " << 42 << endl;

file.close();
cout << "Done writing." << endl;
```

### Reading from a file
```cpp
ifstream file("notes.txt");

if (!file.is_open()) {
    cout << "File not found!" << endl;
    return 1;
}

string line;
while (getline(file, line)) {    // read one line at a time
    cout << line << endl;
}
file.close();
```

### Append mode — add to existing file
```cpp
ofstream file("log.txt", ios::app);  // ios::app = don't erase, add to end
file << "New entry at line 5" << endl;
file.close();
```

### Read numbers from file
```cpp
// Suppose file contains: 10 20 30 40 50
ifstream file("numbers.txt");
int sum = 0, n;
while (file >> n) {    // read numbers one by one
    sum += n;
}
cout << "Sum: " << sum << endl;   // 150
file.close();
```

---

## 15. Error Handling (Exceptions)

**The problem:** Things go wrong at runtime — division by zero, file not found, bad input. Without error handling, your program just crashes.

**The solution:** Throw exceptions when something goes wrong. Catch them and handle gracefully.

```
try {
    // code that might fail
} catch (ExceptionType& e) {
    // handle the failure
}
```

```cpp
#include <stdexcept>
using namespace std;

double safeDivide(double a, double b) {
    if (b == 0) {
        throw runtime_error("Division by zero!");  // throw stops execution
    }
    return a / b;
}

int main() {
    try {
        cout << safeDivide(10, 2) << endl;   // 5 — works
        cout << safeDivide(10, 0) << endl;   // throws exception!
        cout << "Never reached" << endl;
    }
    catch (const runtime_error& e) {
        cout << "Caught error: " << e.what() << endl;
    }

    cout << "Program continues normally here" << endl;
    return 0;
}
```

### Standard exception types

| Exception | Use it when |
|-----------|------------|
| `runtime_error` | General unexpected runtime problem |
| `invalid_argument` | Bad parameter passed to function |
| `out_of_range` | Index/value out of valid range |
| `logic_error` | Programmer logic error |
| `bad_alloc` | Memory allocation failed |

### Custom exception
```cpp
class InsufficientFundsError : public exception {
    string message;
    double amount;
public:
    InsufficientFundsError(double amt) : amount(amt) {
        message = "Insufficient funds: tried to withdraw $" + to_string(amt);
    }
    const char* what() const noexcept override {
        return message.c_str();
    }
};

void withdraw(double balance, double amount) {
    if (amount > balance) {
        throw InsufficientFundsError(amount);
    }
    cout << "Withdrew $" << amount << endl;
}

try {
    withdraw(100.0, 200.0);
} catch (const InsufficientFundsError& e) {
    cout << "Error: " << e.what() << endl;
}
```

---

## 16. The STL — Standard Template Library

**The STL is a ready-made collection of data structures and algorithms.**
No need to build a linked list or a sort yourself — it's all here, tested and fast.

### vector — the go-to container
```cpp
#include <vector>
vector<int> v = {5, 3, 1, 4, 2};

v.push_back(6);            // add to end
v.pop_back();              // remove from end
v.insert(v.begin(), 0);   // add at front
v.erase(v.begin() + 2);   // remove element at index 2

cout << v.size()  << endl; // number of elements
cout << v.empty() << endl; // 0 (not empty)
cout << v[0]      << endl; // first element
cout << v.front() << endl; // first element
cout << v.back()  << endl; // last element

for (int x : v) cout << x << " ";
```

### map — dictionary / key-value pairs
```cpp
#include <map>
map<string, int> ages;

ages["Alice"]   = 25;
ages["Bob"]     = 30;
ages["Charlie"] = 22;

cout << ages["Alice"] << endl;   // 25

// Check if key exists
if (ages.count("Bob")) {
    cout << "Bob is " << ages["Bob"] << endl;
}

// Iterate (sorted alphabetically)
for (auto& pair : ages) {
    cout << pair.first << " → " << pair.second << endl;
}

// Remove
ages.erase("Bob");
cout << ages.size() << endl;   // 2
```

### unordered_map — faster (no sorting)
```cpp
#include <unordered_map>
unordered_map<string, int> wordCount;

string words[] = {"apple","banana","apple","cherry","apple","banana"};
for (string w : words) {
    wordCount[w]++;   // if key doesn't exist, default is 0
}

for (auto& [word, count] : wordCount) {
    cout << word << ": " << count << endl;
}
// apple: 3, banana: 2, cherry: 1
```

### set — unique sorted values
```cpp
#include <set>
set<int> s;
s.insert(5);
s.insert(3);
s.insert(1);
s.insert(3);   // duplicate — ignored
s.insert(5);   // duplicate — ignored

for (int x : s) cout << x << " ";   // 1 3 5 — sorted, no duplicates

cout << s.count(3)  << endl;   // 1 (exists)
cout << s.count(99) << endl;   // 0 (doesn't exist)

s.erase(3);
```

### stack and queue
```cpp
#include <stack>
#include <queue>

// Stack = Last In, First Out (like a pile of plates)
stack<int> st;
st.push(10); st.push(20); st.push(30);
cout << st.top() << endl;   // 30 — look at top
st.pop();                   // remove top
cout << st.top() << endl;   // 20

// Queue = First In, First Out (like a line at a store)
queue<string> q;
q.push("Alice"); q.push("Bob"); q.push("Charlie");
cout << q.front() << endl;   // Alice — look at front
q.pop();                     // remove front
cout << q.front() << endl;   // Bob
```

### Algorithms library
```cpp
#include <algorithm>
#include <numeric>

vector<int> v = {5, 2, 8, 1, 9, 3, 7, 4, 6};

sort(v.begin(), v.end());                       // ascending:  1 2 3 4 5 6 7 8 9
sort(v.begin(), v.end(), greater<int>());        // descending: 9 8 7 6 5 4 3 2 1

int mn    = *min_element(v.begin(), v.end());    // smallest
int mx    = *max_element(v.begin(), v.end());    // largest
int total = accumulate(v.begin(), v.end(), 0);   // sum

// Find
auto it = find(v.begin(), v.end(), 7);
if (it != v.end()) cout << "Found 7!" << endl;

// Count
int cnt = count(v.begin(), v.end(), 5);

// Reverse
reverse(v.begin(), v.end());

// Binary search (array must be sorted first!)
sort(v.begin(), v.end());
bool found = binary_search(v.begin(), v.end(), 5);
```

---

# 🔴 ADVANCED

---

## 17. Templates

**The problem:** You want a `maximum` function that works for int, double, string, any type.
**Without templates:** Write one for each type. Tedious.
**With templates:** Write once, use for any type.

```cpp
// Without templates
int   maxInt   (int a,    int b)    { return a > b ? a : b; }
double maxDouble(double a, double b) { return a > b ? a : b; }
// ... repeat for every type

// WITH templates — one function for everything
template <typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

cout << maximum(3, 7)         << endl;  // 7     (int)
cout << maximum(3.5, 2.1)     << endl;  // 3.5   (double)
cout << maximum('a', 'z')     << endl;  // z     (char)
cout << maximum(string("hi"), string("yo")) << endl;  // yo
```

### Class templates
```cpp
template <typename T>
class Stack {
    vector<T> data;
public:
    void push(T val)  { data.push_back(val); }
    void pop()        { data.pop_back(); }
    T    top()        { return data.back(); }
    bool empty()      { return data.empty(); }
    int  size()       { return data.size(); }
};

Stack<int>    intStack;
Stack<string> strStack;

intStack.push(1); intStack.push(2); intStack.push(3);
cout << intStack.top() << endl;   // 3

strStack.push("hello");
strStack.push("world");
cout << strStack.top() << endl;   // world
```

### Multiple template types
```cpp
template <typename Key, typename Value>
class Pair {
public:
    Key key;
    Value value;

    Pair(Key k, Value v) : key(k), value(v) {}

    void print() {
        cout << key << " : " << value << endl;
    }
};

Pair<string, int>    p1("age", 25);
Pair<int, double>    p2(1, 3.14);
Pair<string, string> p3("name", "Alice");

p1.print();  // age : 25
p2.print();  // 1 : 3.14
p3.print();  // name : Alice
```

---

## 18. Smart Pointers & Memory Management

**The problem with raw pointers:**
```cpp
int* p = new int(5);
// ... 200 lines of code ...
// oops, forgot delete p → memory leak forever!
```

**The solution: smart pointers that delete themselves.**

### unique_ptr — one owner, auto-deleted
```cpp
#include <memory>

// Old way (dangerous):
Dog* d = new Dog("Rex", 3, "Husky");
d->bark();
delete d;   // must remember this!

// New way (safe):
auto d = make_unique<Dog>("Rex", 3, "Husky");
d->bark();
// automatically deleted when d goes out of scope — no delete needed!

// Transfer ownership
auto d2 = move(d);   // d is now null, d2 owns the Dog
// d2.bark();        // works
// d.bark();         // crash — d is null
```

### shared_ptr — multiple owners
```cpp
auto sp1 = make_shared<string>("Hello");
auto sp2 = sp1;     // both own the string, reference count = 2
auto sp3 = sp1;     // count = 3

cout << sp1.use_count() << endl;   // 3
cout << *sp1 << endl;              // Hello

sp1.reset();   // count = 2
sp2.reset();   // count = 1
// string deleted when sp3 goes out of scope (count reaches 0)
```

### weak_ptr — observe without owning
```cpp
auto sp = make_shared<int>(42);
weak_ptr<int> wp = sp;   // doesn't increase ref count

// Try to access
if (auto locked = wp.lock()) {
    cout << *locked << endl;   // 42
} else {
    cout << "Object was deleted" << endl;
}

sp.reset();   // delete the int

if (wp.expired()) {
    cout << "wp sees it's gone" << endl;
}
```

### Stack vs Heap
```
Stack (local variables):        Heap (new/dynamic):
───────────────────────         ───────────────────────
int x = 5;                      int* p = new int(5);
Auto-deleted when out of scope  Must delete manually (or smart ptr)
Very fast                       Slower
Limited size (~1-8 MB)          Large (limited by RAM)
```

---

## 19. Modern C++ (C++11 to C++20)

### auto — let compiler determine type
```cpp
auto x = 42;               // int
auto pi = 3.14;            // double
auto name = string("Bob"); // string

// Super useful with complex types
vector<pair<string, int>> data = {{"a", 1}};
auto it = data.begin();    // much nicer than: vector<pair<string,int>>::iterator it
```

### Lambda functions — tiny anonymous functions
```cpp
// Basic
auto sayHi = []() { cout << "Hi!" << endl; };
sayHi();

// With parameters
auto add = [](int a, int b) { return a + b; };
cout << add(3, 4) << endl;  // 7

// Capture surrounding variables
int x = 10;
auto addX = [x](int n) { return n + x; };  // captures x by value
cout << addX(5) << endl;  // 15

int counter = 0;
auto increment = [&counter]() { counter++; };  // captures by reference
increment(); increment(); increment();
cout << counter << endl;  // 3

// Used with sort
vector<int> v = {3, 1, 4, 1, 5, 9};
sort(v.begin(), v.end(), [](int a, int b) { return a > b; });  // descending
for (int n : v) cout << n << " ";  // 9 5 4 3 1 1
```

### Range-based for with structured bindings (C++17)
```cpp
map<string, int> scores = {{"Alice", 95}, {"Bob", 87}, {"Charlie", 92}};

// Old way
for (auto& pair : scores) {
    cout << pair.first << ": " << pair.second << endl;
}

// New way (C++17) — much cleaner
for (auto& [name, score] : scores) {
    cout << name << ": " << score << endl;
}
```

### Move semantics — avoid expensive copies
```cpp
// When you have a large object and no longer need the source:
vector<int> original(1000000, 42);   // 1 million elements

// COPY — slow: allocates new memory and copies everything
vector<int> copy1 = original;

// MOVE — fast: just transfers the pointer, no copying
vector<int> moved = move(original);
// original is now empty, moved owns the data
```

### std::optional — value that might not exist (C++17)
```cpp
#include <optional>

optional<string> findUser(int id) {
    if (id == 1) return "Alice";
    if (id == 2) return "Bob";
    return nullopt;   // no user found
}

auto user = findUser(1);
if (user) {
    cout << "Found: " << *user << endl;   // Found: Alice
}

auto missing = findUser(99);
cout << missing.value_or("Unknown") << endl;  // Unknown
```

### constexpr — compute at compile time
```cpp
constexpr int factorial(int n) {
    return n <= 1 ? 1 : n * factorial(n - 1);
}

// Computed at compile time — zero runtime cost!
constexpr int f10 = factorial(10);   // 3628800
```

---

## 20. Multithreading

**Running multiple tasks at the same time.**
Instead of: download file, then process it, then send email (sequential)
Do: all three simultaneously!

```cpp
#include <thread>
#include <chrono>
using namespace std;

void task1() {
    cout << "Task 1 starting" << endl;
    this_thread::sleep_for(chrono::seconds(2));
    cout << "Task 1 done!" << endl;
}

void task2() {
    cout << "Task 2 starting" << endl;
    this_thread::sleep_for(chrono::seconds(1));
    cout << "Task 2 done!" << endl;
}

int main() {
    thread t1(task1);   // start task1 in background
    thread t2(task2);   // start task2 in background

    t1.join();          // wait for t1 to finish
    t2.join();          // wait for t2 to finish

    cout << "Both done!" << endl;
    // Total time: ~2 seconds, not 3! (they ran at the same time)
    return 0;
}
```

### mutex — prevent data corruption
```cpp
#include <mutex>

mutex mtx;
int counter = 0;

// Without mutex: two threads might read/write counter simultaneously = wrong result
// With mutex: only one thread at a time can modify counter

void increment() {
    for (int i = 0; i < 1000; i++) {
        lock_guard<mutex> lock(mtx);  // locks mutex, auto-unlocks when done
        counter++;
    }
}

thread t1(increment);
thread t2(increment);
t1.join(); t2.join();
cout << counter << endl;  // guaranteed 2000
```

### async — run and get result later
```cpp
#include <future>

int slowCalculation(int n) {
    this_thread::sleep_for(chrono::seconds(3));
    return n * n * n;
}

// Start in background
auto result = async(launch::async, slowCalculation, 5);

// Do other work while it runs...
cout << "Working on other stuff..." << endl;
this_thread::sleep_for(chrono::seconds(1));
cout << "Still doing stuff..." << endl;

// Get result (waits if not ready)
cout << "Result: " << result.get() << endl;  // 125
```

---

## 21. Best Practices & Common Mistakes

### ✅ Good habits

```cpp
// 1. Always initialize variables
int x = 0;          // not: int x;  (could be garbage)
string s = "";
bool flag = false;

// 2. Use smart pointers — never raw new/delete
auto ptr = make_unique<MyClass>();  // auto-managed

// 3. Pass large objects by const reference
void process(const vector<int>& v);  // not by value (avoids copying)
void display(const string& s);

// 4. Use const for things that don't change
const int MAX = 100;
string getName() const;    // const method — won't modify the object

// 5. Use override when overriding virtual functions
void speak() override;     // compiler error if base doesn't have virtual speak()

// 6. Always virtual destructor in base class
class Base {
public:
    virtual ~Base() {}
};

// 7. Prefer range-based for loops
for (const auto& item : container) { }

// 8. Use nullptr, not NULL or 0
int* p = nullptr;

// 9. Use {} initialization — prevents silent narrowing
int x{42};           // fine
// int y{3.14};      // ERROR — good! catches accidental truncation
```

### ❌ Common mistakes

```cpp
// 1. Memory leak
int* p = new int(5);
// ... forgot delete p → memory grows forever
// FIX: use make_unique

// 2. Using deleted pointer (dangling pointer)
int* p = new int(5);
delete p;
*p = 10;   // UNDEFINED BEHAVIOR — may crash or silently corrupt data
// FIX: set p = nullptr after delete, or use smart pointers

// 3. Array out of bounds
int arr[5];
arr[5] = 99;   // UNDEFINED BEHAVIOR — valid range is 0-4
// FIX: use vector with .at() which checks bounds

// 4. Missing virtual destructor
class Base { ~Base() {} };         // wrong
class Base { virtual ~Base() {} }; // correct

// 5. Floating point comparison
if (0.1 + 0.2 == 0.3) { }   // FALSE — floating point isn't exact!
// FIX:
const double EPSILON = 1e-9;
if (abs(0.1 + 0.2 - 0.3) < EPSILON) { }  // correct

// 6. Forgetting break in switch
switch (n) {
    case 1: cout << "one";   // falls into case 2 by accident!
    case 2: cout << "two";   // always add break
}

// 7. Object slicing
class Base { int x; };
class Derived : public Base { int y; };
Derived d;
Base b = d;    // y is LOST — "sliced off"
// FIX: use pointers or references for polymorphism
Base& ref = d;    // no slicing

// 8. Uninitialized variable
int x;
cout << x;   // garbage value — could print anything
```

### Compiler flags to use
```bash
# Development (catch bugs early)
g++ -std=c++17 -Wall -Wextra -g -o program main.cpp

# Check for memory issues
g++ -fsanitize=address,undefined -g -o program main.cpp

# Release (production-ready, optimized)
g++ -std=c++17 -O2 -o program main.cpp
```

---

## 22. Quick Reference Cheat Sheet

### Type sizes and ranges

| Type | Size | Range / Notes |
|------|------|---------------|
| `int` | 4 bytes | -2,147,483,648 to 2,147,483,647 |
| `long long` | 8 bytes | ±9.2 × 10^18 |
| `double` | 8 bytes | ~15 decimal digits |
| `float` | 4 bytes | ~7 decimal digits |
| `char` | 1 byte | single character |
| `bool` | 1 byte | true or false |

### Useful math functions (`#include <cmath>`)
```cpp
sqrt(x)      // square root
pow(x, y)    // x to the power y
abs(x)       // absolute value
floor(x)     // round down
ceil(x)      // round up
round(x)     // round to nearest
sin/cos/tan  // trig functions
log(x)       // natural log
log10(x)     // log base 10
```

### Which container to use?

| Situation | Use |
|-----------|-----|
| Ordered list, fast access by index | `vector` |
| Key-value pairs, sorted | `map` |
| Key-value pairs, fast lookup | `unordered_map` |
| Unique items, sorted | `set` |
| Unique items, fast lookup | `unordered_set` |
| LIFO (undo, backtracking) | `stack` |
| FIFO (task queue, BFS) | `queue` |
| Priority processing | `priority_queue` |

### String methods
```cpp
s.length()          // length
s.empty()           // is empty?
s.substr(pos, len)  // extract part
s.find(sub)         // find position (string::npos if not found)
s.replace(pos, len, newStr)
s + t               // concatenate
s += t              // append
stoi(s)             // string to int
stod(s)             // string to double
to_string(n)        // number to string
```

### Common headers
```cpp
#include <iostream>       // cout, cin
#include <string>         // string
#include <vector>         // vector
#include <map>            // map
#include <unordered_map>  // unordered_map
#include <set>            // set
#include <stack>          // stack
#include <queue>          // queue, priority_queue
#include <algorithm>      // sort, find, etc.
#include <numeric>        // accumulate, etc.
#include <cmath>          // sqrt, pow, etc.
#include <memory>         // smart pointers
#include <fstream>        // file I/O
#include <sstream>        // string streams
#include <stdexcept>      // exceptions
#include <thread>         // multithreading
#include <optional>       // optional (C++17)
```

---

*You made it. Now write code. Break things. Fix them. That's how you actually learn C++.*
