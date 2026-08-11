# C++ Fundamentals for DSA
## Variables, Data Types, Type Casting & Operators

Before learning DSA, you need a strong understanding of these C++ fundamentals because almost every DSA program uses **variables, data types, operators, conditions, loops, arrays, pointers, and functions**.

---

# 1. Preprocessor Directive

```cpp
#include <iostream>
```

### What is `#include <iostream>`?

`#include` is a **preprocessor directive**.

It tells the C++ preprocessor to include the contents of the specified header file before compilation.

`iostream` stands for:

> **Input Output Stream**

It provides objects such as:

- `cout` → output
- `cin` → input
- `cerr` → error output
- `clog` → logging output

Example:

```cpp
#include <iostream>

int main() {
    std::cout << "Hello World";
    return 0;
}
```

---

# 2. Namespace

```cpp
using namespace std;
```

The C++ Standard Library contains many names inside the `std` namespace.

For example:

```cpp
std::cout
std::cin
std::endl
std::string
```

If we write:

```cpp
using namespace std;
```

we can directly write:

```cpp
cout
cin
endl
string
```

### Without `using namespace std`

```cpp
#include <iostream>

int main() {
    std::cout << "Hello";
    return 0;
}
```

### With it

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello";
    return 0;
}
```

### Important recommendation

For small DSA programs, this is commonly used:

```cpp
using namespace std;
```

But in larger projects, it is generally safer to avoid importing the entire namespace and instead use:

```cpp
std::cout
std::vector
std::string
```

This prevents **name conflicts**.

---

# 3. `main()` Function

Every normal C++ executable program needs an entry point.

```cpp
int main() {

    return 0;
}
```

Program execution starts from:

```cpp
main()
```

### Why `int`?

`main()` returns an integer to the operating system.

```cpp
return 0;
```

generally means:

> Program executed successfully.

---

# 4. Printing Output

C++ uses `cout` for standard output.

```cpp
cout << "Hello";
```

The `<<` operator sends data to `cout`.

Example:

```cpp
int age = 20;

cout << age;
```

Output:

```text
20
```

You can print multiple things:

```cpp
cout << "Age: " << age;
```

Output:

```text
Age: 20
```

---

# 5. New Line: `endl` vs `\n`

There are two common ways to move to the next line.

## Using `endl`

```cpp
cout << "Hello" << endl;
cout << "World";
```

Output:

```text
Hello
World
```

## Using `\n`

```cpp
cout << "Hello\n";
cout << "World";
```

Output:

```text
Hello
World
```

### Important difference

`endl`:

1. Inserts a new line.
2. Flushes the output buffer.

`\n`:

1. Inserts a new line.
2. Does not force a flush.

Therefore, in competitive programming and DSA, `\n` is generally preferred when you only need a new line.

```cpp
cout << "Hello\n";
```

---

# 6. Variables

## Definition

A **variable** is a named memory location used to store a value that can be accessed and, depending on its declaration, modified during program execution.

Example:

```cpp
int age = 20;
```

Here:

| Part | Meaning |
|---|---|
| `int` | Data type |
| `age` | Variable name |
| `=` | Assignment operator |
| `20` | Initial value |

Conceptually:

```text
Memory
┌──────────────┐
│ age = 20     │
└──────────────┘
```

The variable `age` gives us a convenient name through which we can access the stored value.

---

# 7. Declaration vs Initialization

These two concepts are different.

## Declaration

```cpp
int age;
```

We are telling C++:

> Create a variable named `age` of type `int`.

## Initialization

```cpp
int age = 20;
```

The variable is created and given its initial value.

### Assignment

```cpp
int age = 20;

age = 25;
```

Here:

```cpp
age = 25;
```

is **assignment**, not initialization.

So:

```cpp
int age = 20;   // initialization
age = 25;       // assignment
```

---

# 8. Identifiers

## Definition

An **identifier** is a name used to identify programming entities such as:

- variables
- functions
- classes
- objects
- structures
- namespaces

Example:

```cpp
int age;

void calculateSum();

class Student;
```

Here:

```text
age          → identifier
calculateSum → identifier
Student      → identifier
```

---

# 9. Rules for Identifiers

An identifier:

### Rule 1 — Can contain letters

```cpp
int age;
int studentName;
```

### Rule 2 — Can contain digits

```cpp
int student1;
int marks2026;
```

But it **cannot start with a digit**.

❌ Invalid:

```cpp
int 1student;
```

✅ Valid:

```cpp
int student1;
```

### Rule 3 — Underscore is allowed

```cpp
int student_name;
```

### Rule 4 — Spaces are not allowed

❌

```cpp
int student name;
```

✅

```cpp
int student_name;
```

### Rule 5 — C++ is case-sensitive

These are different:

```cpp
age
Age
AGE
```

### Rule 6 — Keywords cannot be used as identifiers

❌

```cpp
int class;
```

because `class` is a C++ keyword.

---

# 10. Data Types

## Definition

A **data type** tells the compiler:

1. What kind of value a variable can store.
2. How that value should be interpreted.
3. Usually, how much memory is required for the object.

Common C++ data types include:

```text
int
float
double
char
bool
string
```

---

# 11. Fundamental Data Types

## 11.1 `int`

Used for whole numbers.

```cpp
int age = 20;
int marks = 95;
int temperature = -5;
```

Examples:

```text
10
0
-20
1000
```

Not appropriate for:

```text
10.5
3.14
```

---

# 12. `float`

Used for floating-point/decimal values.

```cpp
float price = 10.5f;
```

The `f` suffix explicitly makes the literal a `float`.

Example:

```cpp
float percentage = 85.5f;
```

---

# 13. `double`

Also stores floating-point values, generally with more precision than `float`.

```cpp
double price = 10.5;
```

Example:

```cpp
double pi = 3.141592653589793;
```

In many programs, `double` is preferred over `float` when you need ordinary floating-point calculations.

---

# 14. `char`

Stores a single character.

```cpp
char grade = 'A';
```

Characters use **single quotes**:

```cpp
'A'
'b'
'7'
'#'
```

This is different from a string.

```cpp
char ch = 'A';        // one character
string name = "Ravi"; // multiple characters
```

---

# 15. `bool`

Stores a logical value:

```cpp
true
false
```

Example:

```cpp
bool isLoggedIn = true;
bool isPassed = false;
```

When printed normally:

```cpp
cout << true;
```

the output is:

```text
1
```

and:

```cpp
cout << false;
```

outputs:

```text
0
```

You can use:

```cpp
cout << boolalpha;
```

to display:

```text
true
false
```

---

# 16. `string`

`string` is used to store text.

```cpp
string name = "Ravi";
```

You normally need:

```cpp
#include <string>
```

although `iostream` may indirectly make it available in some implementations.

Example:

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {

    string name = "Ravi";

    cout << name;

    return 0;
}
```

---

# 17. Typical Size of Data Types

You can use:

```cpp
sizeof()
```

to determine the size of an object/type in bytes.

Example:

```cpp
cout << sizeof(int);
```

On many modern systems:

| Data Type | Typical Size |
|---|---:|
| `char` | 1 byte |
| `bool` | typically 1 byte |
| `int` | 4 bytes |
| `float` | 4 bytes |
| `double` | 8 bytes |

### Important

Do **not** memorize these as universal guarantees.

The C++ standard defines minimum requirements and relationships, while the actual size depends on the implementation/platform.

For example:

```cpp
cout << sizeof(int);
```

is better than assuming:

```text
int = always 4 bytes
```

---

# 18. `sizeof()` Operator

`sizeof` determines the size of an object or type in bytes.

Example:

```cpp
int x = 10;

cout << sizeof(x);
```

You can also use:

```cpp
cout << sizeof(int);
```

For arrays:

```cpp
int arr[5];

cout << sizeof(arr);
```

If `int` is 4 bytes, then:

```text
5 × 4 = 20 bytes
```

This becomes extremely important in DSA when working with:

- arrays
- structures
- memory
- pointers
- dynamic allocation

---

# 19. Type Conversion

## Definition

**Type conversion** means converting a value from one data type to another.

For example:

```cpp
int x = 10;
double y = x;
```

Here:

```text
int → double
```

---

# 20. Implicit Type Conversion

When C++ automatically converts one type to another, it is called **implicit conversion**.

Example:

```cpp
int x = 10;

double y = x;
```

Conceptually:

```text
10 (int)
 ↓
10.0 (double)
```

Another example:

```cpp
int a = 10;
double b = 3.5;

double result = a + b;
```

C++ converts `a` to a suitable floating-point type for the operation.

---

# 21. Explicit Type Conversion / Type Casting

When we explicitly tell C++ to convert a value, it is called **explicit conversion** or **type casting**.

Example:

```cpp
double price = 10.5;

int newPrice = static_cast<int>(price);
```

Result:

```text
newPrice = 10
```

The fractional part is discarded.

It does **not** round:

```text
10.5 → 10
10.9 → 10
10.1 → 10
```

---

# 22. C++ Type-Casting Styles

There are several casts in C++.

## 1. `static_cast`

Used for many ordinary compile-time conversions.

```cpp
double price = 10.5;

int x = static_cast<int>(price);
```

Preferred for ordinary numeric conversions.

---

## 2. C-style cast

```cpp
int x = (int)price;
```

This is older C/C++ syntax.

It works, but modern C++ generally prefers:

```cpp
int x = static_cast<int>(price);
```

because the conversion is more explicit.

---

## 3. `dynamic_cast`

Used primarily for safe runtime casting within polymorphic class hierarchies.

Example:

```cpp
Base* ptr = new Derived();

Derived* d = dynamic_cast<Derived*>(ptr);
```

This is **not** a general-purpose numeric conversion tool.

So saying:

> "Use dynamic_cast to convert int to float"

is incorrect.

---

## 4. `const_cast`

Used to add/remove `const` qualification from a type.

```cpp
const int x = 10;
```

`const_cast` is mainly relevant to advanced C++ programming and should not be confused with ordinary numeric conversion.

---

## 5. `reinterpret_cast`

Used for low-level reinterpretation of object representations/pointer types.

It is an advanced and potentially dangerous operation.

It is **not** a normal way to convert:

```text
int → float
```

---

# 23. Important Correction About Type Conversion

It is incorrect to say:

> "Conversion is only possible between compatible types."

C++ has many conversion rules, and some conversions are allowed even when the result may be surprising or lossy.

For example:

```cpp
int x = 65;

char ch = static_cast<char>(x);
```

Depending on the character encoding, this can represent `'A'`.

Also:

```cpp
double x = 10.9;

int y = static_cast<int>(x);
```

produces:

```text
10
```

So the important question is not simply:

> "Can C++ convert these types?"

but:

> **"What conversion rules apply, and what information might be lost?"**

---

# 24. Operators

## Definition

An **operator** is a symbol or syntactic construct that tells C++ to perform an operation on one or more operands.

Example:

```cpp
a + b
```

Here:

```text
a, b → operands
+    → operator
```

---

# 25. Main Categories of Operators

C++ operators can broadly be classified into:

1. Arithmetic
2. Relational / Comparison
3. Logical
4. Assignment
5. Increment / Decrement
6. Bitwise
7. Conditional
8. Unary
9. Other/special operators

---

# 26. Arithmetic Operators

Arithmetic operators perform mathematical operations.

| Operator | Meaning |
|---|---|
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Division |
| `%` | Modulus/remainder |
| `++` | Increment |
| `--` | Decrement |

Example:

```cpp
int a = 10;
int b = 3;

cout << a + b; // 13
cout << a - b; // 7
cout << a * b; // 30
cout << a / b; // 3
cout << a % b; // 1
```

---

# 27. Integer Division — VERY IMPORTANT

This is one of the most important concepts for DSA.

If both operands are integers:

```cpp
int a = 10;
int b = 3;

cout << a / b;
```

Output:

```text
3
```

Not:

```text
3.333333
```

Why?

Because both operands are integers, so the operation uses integer division.

Conceptually:

```text
10 / 3 = 3 remainder 1
```

The fractional part is discarded.

---

# 28. Floating-Point Division

If at least one operand is floating-point:

```cpp
double a = 10;
double b = 3;

cout << a / b;
```

Result is approximately:

```text
3.33333
```

Similarly:

```cpp
int a = 10;
double b = 3;

cout << a / b;
```

produces floating-point division.

### Remember

```text
int / int       → integer division
int / double    → floating-point result
double / int    → floating-point result
double / double → floating-point result
```

More generally, the exact result type follows C++'s usual arithmetic conversions.

---

# 29. Modulus `%`

The modulus operator gives the remainder of integer division.

```cpp
10 % 3
```

Result:

```text
1
```

Because:

```text
10 = 3 × 3 + 1
```

Another example:

```cpp
17 % 5
```

Result:

```text
2
```

### DSA applications

`%` is extremely important.

It is commonly used for:

- checking even/odd
- digit extraction
- circular arrays
- hashing
- cyclic indexing
- mathematical problems

Example:

```cpp
if (n % 2 == 0)
    cout << "Even";
else
    cout << "Odd";
```

---

# 30. Relational / Comparison Operators

These compare two values.

| Operator | Meaning |
|---|---|
| `<` | Less than |
| `>` | Greater than |
| `<=` | Less than or equal to |
| `>=` | Greater than or equal to |
| `==` | Equal to |
| `!=` | Not equal to |

Example:

```cpp
int a = 10;
int b = 20;

cout << (a < b);
```

Output:

```text
1
```

because:

```text
10 < 20
```

is true.

---

# 31. `=` vs `==`

This is one of the most common beginner mistakes.

### `=`

Assignment:

```cpp
x = 10;
```

Means:

> Put 10 into x.

### `==`

Comparison:

```cpp
x == 10
```

Means:

> Is x equal to 10?

Example:

```cpp
if (x == 10) {
    cout << "Yes";
}
```

Do not confuse:

```cpp
x = 10;
```

with:

```cpp
x == 10;
```

---

# 32. Logical Operators

Logical operators combine or modify conditions.

| Operator | Meaning |
|---|---|
| `&&` | AND |
| `||` | OR |
| `!` | NOT |

---

# 33. Logical AND `&&`

Both conditions must be true.

```cpp
int age = 20;

if (age >= 18 && age <= 60) {
    cout << "Valid";
}
```

Truth table:

| A | B | A && B |
|---|---|---|
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

---

# 34. Logical OR `||`

At least one condition must be true.

```cpp
if (marks >= 90 || attendance >= 90) {
    cout << "Eligible";
}
```

Truth table:

| A | B | A \|\| B |
|---|---|---|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

---

# 35. Logical NOT `!`

Reverses a boolean condition.

```cpp
bool isReady = true;

cout << !isReady;
```

Result:

```text
false
```

Conceptually:

```text
true  → ! → false
false → ! → true
```

---

# 36. Short-Circuit Evaluation

This is an important concept for DSA.

For:

```cpp
A && B
```

if `A` is false, C++ may not evaluate `B`.

For:

```cpp
A || B
```

if `A` is true, C++ may not evaluate `B`.

Example:

```cpp
if (ptr != nullptr && ptr->data == 10) {
    ...
}
```

The first condition:

```cpp
ptr != nullptr
```

is checked first.

If it is false, C++ does not evaluate:

```cpp
ptr->data
```

This can prevent invalid pointer access.

---

# 37. Bitwise Operators

Bitwise operators operate on the individual bits of integral values.

| Operator | Meaning |
|---|---|
| `&` | Bitwise AND |
| `|` | Bitwise OR |
| `^` | Bitwise XOR |
| `~` | Bitwise NOT |
| `<<` | Left shift |
| `>>` | Right shift |

These are extremely important in advanced DSA, competitive programming, and low-level programming.

---

# 38. Binary Representation

Consider:

```text
5 = 0101
3 = 0011
```

### Bitwise AND

```text
0101
0011
----
0001
```

Therefore:

```cpp
5 & 3
```

gives:

```text
1
```

---

# 39. Bitwise OR

```text
0101
0011
----
0111
```

Therefore:

```cpp
5 | 3
```

gives:

```text
7
```

---

# 40. Bitwise XOR

XOR produces `1` when the corresponding bits are different.

```text
0101
0011
----
0110
```

Therefore:

```cpp
5 ^ 3
```

gives:

```text
6
```

### XOR truth table

| A | B | A ^ B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

XOR becomes very important in DSA problems involving:

- unique elements
- duplicate cancellation
- bit manipulation
- subsets
- XOR tricks

---

# 41. Bitwise NOT `~`

`~` flips every bit of its operand.

```text
0 → 1
1 → 0
```

Example:

```cpp
int x = 5;

cout << ~x;
```

The exact result involves the representation of signed integers and should not be memorized using a simplistic "just flip the four visible bits" model.

For typical two's-complement systems:

```text
~x = -x - 1
```

so:

```text
~5 = -6
```

---

# 42. Left Shift `<<`

Left shift moves bits toward the left.

```cpp
5 << 1
```

Binary:

```text
0101
```

Shift left:

```text
1010
```

which represents:

```text
10
```

For suitable nonnegative values and within the relevant range:

```text
x << 1 ≈ x × 2
```

---

# 43. Right Shift `>>`

Right shift moves bits toward the right.

```cpp
10 >> 1
```

Binary:

```text
1010
```

After shifting:

```text
0101
```

Result:

```text
5
```

For suitable nonnegative values:

```text
x >> 1 ≈ x / 2
```

But be careful with signed negative values because right-shift behavior depends on the language rules and implementation details.

---

# 44. Unary Operators

## Definition

A **unary operator** operates on a single operand.

Example:

```cpp
-x
```

Here:

```text
-  → operator
x  → operand
```

Common unary operators include:

```text
+
-
++
--
!
~
```

But classification depends on context: operators such as `+`, `-`, `*`, `&`, and `<<` can have different meanings depending on how they are used.

---

# 45. Unary Plus and Minus

```cpp
int x = 10;

cout << +x; // 10
cout << -x; // -10
```

`-x` changes the sign of the value.

---

# 46. Increment Operator `++`

Increases a variable by 1.

```cpp
int x = 5;

x++;
```

Now:

```text
x = 6
```

There are two forms:

```cpp
++x;  // pre-increment
x++;  // post-increment
```

---

# 47. Pre-Increment

```cpp
int x = 5;

int y = ++x;
```

Execution:

```text
x = 5
     ↓
++x
     ↓
x = 6
     ↓
y = 6
```

Final:

```text
x = 6
y = 6
```

### Rule

> **Pre-increment: increment first, then use the value.**

---

# 48. Post-Increment

```cpp
int x = 5;

int y = x++;
```

Execution:

```text
x = 5
     ↓
use old value → y = 5
     ↓
increment x
     ↓
x = 6
```

Final:

```text
x = 6
y = 5
```

### Rule

> **Post-increment: use the old value first, then increment.**

---

# 49. Pre vs Post Increment

| Expression | What happens first? | Example result |
|---|---|---|
| `++x` | Increment | `y` gets new value |
| `x++` | Use old value | `y` gets old value |

Example:

```cpp
int x = 10;

cout << ++x;
```

Output:

```text
11
```

But:

```cpp
int x = 10;

cout << x++;
```

Output:

```text
10
```

Afterward:

```text
x = 11
```

---

# 50. Decrement Operator `--`

Decreases a variable by 1.

```cpp
int x = 5;

x--;
```

Now:

```text
x = 4
```

Just like increment, it has:

```cpp
--x;  // pre-decrement
x--;  // post-decrement
```

---

# 51. Pre-Decrement

```cpp
int x = 5;

int y = --x;
```

Final:

```text
x = 4
y = 4
```

The variable is decremented before its value is used.

---

# 52. Post-Decrement

```cpp
int x = 5;

int y = x--;
```

Final:

```text
x = 4
y = 5
```

The old value is used first, then the variable is decremented.

---

# 53. Assignment Operators

Assignment operators assign values to variables.

Basic assignment:

```cpp
=
```

Example:

```cpp
int x = 10;
```

Compound assignment operators:

| Operator | Meaning |
|---|---|
| `=` | Assign |
| `+=` | Add and assign |
| `-=` | Subtract and assign |
| `*=` | Multiply and assign |
| `/=` | Divide and assign |
| `%=` | Modulus and assign |
| `&=` | Bitwise AND and assign |
| `|=` | Bitwise OR and assign |
| `^=` | XOR and assign |
| `<<=` | Left shift and assign |
| `>>=` | Right shift and assign |

Example:

```cpp
int x = 10;

x += 5;
```

Equivalent to:

```cpp
x = x + 5;
```

Result:

```text
15
```

---

# 54. Conditional / Ternary Operator

The ternary operator is:

```cpp
condition ? value1 : value2
```

Example:

```cpp
int age = 20;

string result = (age >= 18) ? "Adult" : "Minor";
```

If condition is true:

```text
Adult
```

Otherwise:

```text
Minor
```

It is called the **ternary operator** because it operates on three expressions.

---

# 55. Operator Classification by Number of Operands

Operators can also be classified based on the number of operands.

## Unary

One operand:

```cpp
-x
++x
!x
~x
```

## Binary

Two operands:

```cpp
a + b
a * b
a > b
a && b
```

## Ternary

Three operands:

```cpp
condition ? a : b
```

---

# 56. Operator Precedence

When multiple operators appear in one expression, C++ follows rules that determine which operations are performed first.

Example:

```cpp
int result = 2 + 3 * 4;
```

Multiplication happens before addition.

Therefore:

```text
3 × 4 = 12
2 + 12 = 14
```

Result:

```text
14
```

Not:

```text
20
```

---

# 57. Parentheses Remove Confusion

Instead of relying heavily on precedence:

```cpp
int result = 2 + (3 * 4);
```

Use parentheses when the expression may be difficult to read.

Example:

```cpp
if ((a > b) && (b > c)) {
    ...
}
```

This makes the logic clearer.

---

# 58. Common Mistakes

## Mistake 1 — Using `=` instead of `==`

❌

```cpp
if (x = 10)
```

This performs assignment.

Usually you wanted:

```cpp
if (x == 10)
```

---

## Mistake 2 — Expecting decimal output from integer division

❌

```cpp
int a = 5;
int b = 2;

cout << a / b;
```

Output:

```text
2
```

If you need:

```text
2.5
```

use:

```cpp
cout << static_cast<double>(a) / b;
```

---

## Mistake 3 — Thinking casting rounds

```cpp
double x = 9.99;

int y = static_cast<int>(x);
```

Result:

```text
9
```

It does not round to 10.

---

## Mistake 4 — Confusing `%` with percentage

```cpp
17 % 5
```

does not mean percentage.

It means:

> remainder after integer division.

Result:

```text
2
```

---

## Mistake 5 — Confusing `&&` and `&`

```cpp
&&
```

is **logical AND**.

```cpp
&
```

is **bitwise AND**.

Example:

```cpp
if (a > 0 && b > 0)
```

uses logical AND.

But:

```cpp
a & b
```

uses bitwise AND.

---

## Mistake 6 — Confusing `||` and `|`

```cpp
||
```

→ logical OR

```cpp
|
```

→ bitwise OR

---

## Mistake 7 — Confusing pre and post increment

```cpp
int x = 5;

cout << ++x;
```

prints:

```text
6
```

while:

```cpp
int x = 5;

cout << x++;
```

prints:

```text
5
```

but afterward:

```text
x = 6
```

---

## Mistake 8 — Assuming all data types have fixed sizes

Don't blindly assume:

```text
int = 4 bytes
long = 8 bytes
```

Always remember that exact sizes depend on the implementation.

Use:

```cpp
sizeof(type)
```

when the actual size matters.

---

# 59. Quick Comparison Table

| Concept | Meaning | Example |
|---|---|---|
| Variable | Named storage/object | `int x = 10;` |
| Identifier | Name used for a program entity | `x` |
| Data type | Defines type of value/object | `int` |
| Declaration | Introduces a variable | `int x;` |
| Initialization | Gives initial value | `int x = 10;` |
| Assignment | Changes/stores a value | `x = 20;` |
| Type conversion | Changes value to another type | `double → int` |
| Operator | Performs an operation | `+` |
| Operand | Value operated on | `a` in `a+b` |
| Unary | One operand | `++x` |
| Binary | Two operands | `a+b` |
| Ternary | Three expressions | `a ? b : c` |

---

# 60. Operator Cheat Sheet

| Category | Operators |
|---|---|
| Arithmetic | `+ - * / %` |
| Increment/Decrement | `++ --` |
| Relational | `< > <= >= == !=` |
| Logical | `&& || !` |
| Bitwise | `& \| ^ ~ << >>` |
| Assignment | `= += -= *= /= %= &= \|= ^= <<= >>=` |
| Conditional | `?:` |

---

# 61. DSA-Relevant Concepts You Must Master

Before moving deeply into DSA, make sure these are completely clear:

### Essential

```text
Variables
↓
Data Types
↓
Input / Output
↓
Operators
↓
Conditions
↓
Loops
↓
Functions
↓
Arrays
↓
Strings
↓
Pointers
↓
References
↓
Dynamic Memory
↓
Structures / Classes
```

Especially focus on:

### 1. Integer division

```cpp
7 / 2 = 3
```

### 2. Modulus

```cpp
7 % 2 = 1
```

### 3. Type casting

```cpp
static_cast<double>(a)
```

### 4. Increment/decrement

```cpp
++i
i++
--i
i--
```

### 5. Comparison

```cpp
==
!=
<
>
<=
>=
```

### 6. Logical operations

```cpp
&&
||
!
```

### 7. Bit manipulation

```cpp
&
|
^
~
<<
>>
```

These concepts will appear repeatedly when you study:

- Arrays
- Searching
- Sorting
- Linked Lists
- Stacks
- Queues
- Trees
- Graphs
- Recursion
- Dynamic Programming
- Bit Manipulation
- Competitive Programming

---

# 62. Final Mental Model

Think of a C++ program like this:

```text
                    C++ PROGRAM
                         │
          ┌──────────────┼──────────────┐
          ↓              ↓              ↓
      VARIABLES       FUNCTIONS       OBJECTS
          │
          ↓
     DATA TYPES
          │
     ┌────┼────┐
     ↓    ↓    ↓
    int double char
     │
     ↓
    VALUES
     │
     ↓
  OPERATORS
     │
 ┌───┼───────────────┐
 ↓   ↓       ↓       ↓
+ - * /    < > ==   && ||
              │
              ↓
          CONDITIONS
              │
              ↓
            LOOPS
              │
              ↓
          DATA STRUCTURES
              │
              ↓
              DSA
```

The important point is that **DSA is not isolated from C++ fundamentals**.

When you later write:

```cpp
for (int i = 0; i < n; i++) {
    if (arr[i] % 2 == 0) {
        cout << arr[i] << "\n";
    }
}
```

you are simultaneously using:

- variable declaration
- `int`
- initialization
- comparison
- increment
- loop
- array indexing
- modulus
- equality comparison
- `if`
- output

So mastering these fundamentals will make the actual DSA concepts much easier.