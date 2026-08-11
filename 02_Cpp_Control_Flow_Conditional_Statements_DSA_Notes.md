# C++ Control Flow & Conditional Statements

## DSA Foundation Notes

These notes cover **conditional statements, control flow, `switch-case`,
ternary operator, loop-control statements, exception handling basics,
and ASCII characters**.

------------------------------------------------------------------------

# 1. What is Control Flow?

### Definition

**Control flow** is the order in which statements of a program are
executed.

Normally, a C++ program executes statements from:

``` text
top → bottom
```

But real programs need to make decisions, repeat operations, skip
operations, or exit from a section of code.

For example:

``` text
If marks >= 40
    Student passes
Otherwise
    Student fails
```

C++ provides control-flow constructs that allow us to:

-   make decisions
-   repeat operations
-   skip operations
-   terminate loops
-   return from functions
-   jump to labels
-   handle exceptions

For DSA, conditional statements are extremely important because almost
every algorithm contains decision-making.

------------------------------------------------------------------------

# 2. Decision-Making Statements

The main decision-making constructs are:

``` text
if
if-else
else-if ladder
nested if
switch-case
ternary operator
```

### Important terminology correction

It is better to distinguish between:

-   `if`, `else`, `else if` → conditional/control-flow statements
-   `switch`, `case`, `default` → selection/control-flow constructs
-   `?:` → conditional/ternary operator

------------------------------------------------------------------------

# 3. `if` Statement

## Definition

The `if` statement executes a block of code **only when its condition
evaluates to true**.

### Syntax

``` cpp
if (condition) {
    // statements
}
```

### Example

``` cpp
int age = 20;

if (age >= 18) {
    cout << "Adult";
}
```

### Dry Run

``` text
age = 20

20 >= 18 ?
     ↓
   true
     ↓
execute if block
     ↓
"Adult"
```

Output:

``` text
Adult
```

If:

``` cpp
int age = 15;
```

then:

``` text
15 >= 18 → false
```

The body of `if` is skipped.

------------------------------------------------------------------------

# 4. What is a Condition?

A **condition** is an expression whose result can be interpreted as true
or false.

Example:

``` cpp
age >= 18
```

The result is either:

``` text
true
```

or:

``` text
false
```

Conditions commonly use relational operators:

``` cpp
<
>
<=
>=
==
!=
```

and logical operators:

``` cpp
&&
||
!
```

Example:

``` cpp
if (age >= 18 && age <= 60) {
    cout << "Valid";
}
```

------------------------------------------------------------------------

# 5. Boolean Conditions in C++

C++ does not require an `if` condition to literally have type `bool`.

For example:

``` cpp
if (5) {
    cout << "Hello";
}
```

This executes because a nonzero value is treated as true.

Conceptually:

``` text
0        → false
non-zero → true
```

Example:

``` cpp
if (0) {
    cout << "A";
}
```

Nothing is printed.

But:

``` cpp
if (-10) {
    cout << "B";
}
```

prints:

``` text
B
```

This is useful when reading DSA code.

------------------------------------------------------------------------

# 6. `if-else`

## Definition

`if-else` provides two possible execution paths.

### Syntax

``` cpp
if (condition) {
    // true block
}
else {
    // false block
}
```

### Example

``` cpp
int number = 7;

if (number % 2 == 0) {
    cout << "Even";
}
else {
    cout << "Odd";
}
```

### Dry Run

``` text
number = 7

7 % 2 == 0
      ↓
    1 == 0
      ↓
    false
      ↓
else executes
      ↓
    "Odd"
```

Output:

``` text
Odd
```

------------------------------------------------------------------------

# 7. `else`

`else` is associated with an `if`.

Invalid:

``` cpp
else {
    cout << "Hello";
}
```

Correct:

``` cpp
if (condition) {
    ...
}
else {
    ...
}
```

### Important

You cannot have an independent `else` without a corresponding `if`.

------------------------------------------------------------------------

# 8. `else if`

When there are multiple possible conditions, use an **else-if ladder**.

### Syntax

``` cpp
if (condition1) {

}
else if (condition2) {

}
else if (condition3) {

}
else {

}
```

### Example

``` cpp
int marks = 75;

if (marks >= 90) {
    cout << "A";
}
else if (marks >= 80) {
    cout << "B";
}
else if (marks >= 70) {
    cout << "C";
}
else {
    cout << "D";
}
```

Output:

``` text
C
```

------------------------------------------------------------------------

# 9. How `else-if` Works

C++ checks conditions **from top to bottom**.

``` text
condition 1?
   ↓
 true → execute → stop checking chain
 false
   ↓
condition 2?
   ↓
 true → execute → stop
 false
   ↓
condition 3?
```

Once one condition is true, the remaining `else if` conditions are
skipped.

### Example

``` cpp
int x = 10;

if (x > 0) {
    cout << "Positive";
}
else if (x > 5) {
    cout << "Greater than 5";
}
```

Output:

``` text
Positive
```

Although `x > 5` is also true, the second condition is never checked
because the first condition already matched.

------------------------------------------------------------------------

# 10. Order of Conditions Matters

Consider:

``` cpp
int marks = 95;

if (marks >= 40) {
    cout << "Pass";
}
else if (marks >= 90) {
    cout << "Excellent";
}
```

Output:

``` text
Pass
```

The second condition never gets a chance.

### Correct ordering

``` cpp
if (marks >= 90) {
    cout << "Excellent";
}
else if (marks >= 40) {
    cout << "Pass";
}
else {
    cout << "Fail";
}
```

### DSA Lesson

When using an `else-if` ladder, **order your conditions carefully**.

------------------------------------------------------------------------

# 11. Nested `if`

## Definition

An `if` statement placed inside another `if` or `else` block is called a
**nested if**.

Example:

``` cpp
int age = 20;
bool hasID = true;

if (age >= 18) {

    if (hasID) {
        cout << "Entry allowed";
    }

}
```

Structure:

``` text
if age >= 18
│
└── if hasID
    │
    └── Entry allowed
```

------------------------------------------------------------------------

# 12. Nested `if` vs Logical `&&`

The same basic logic can often be written using `&&`.

### Nested version

``` cpp
if (age >= 18) {
    if (hasID) {
        cout << "Allowed";
    }
}
```

### Logical version

``` cpp
if (age >= 18 && hasID) {
    cout << "Allowed";
}
```

### Which should you use?

Use `&&` when the conditions naturally form **one combined condition**.

Use nested `if` when the second decision logically depends on entering
the first branch or when separate processing is required.

------------------------------------------------------------------------

# 13. `switch-case`

## Definition

`switch` is a selection statement used to choose among multiple branches
based on the value of an expression.

### Syntax

``` cpp
switch (expression) {

    case value1:
        // code
        break;

    case value2:
        // code
        break;

    default:
        // code
}
```

### Example

``` cpp
int day = 2;

switch (day) {

    case 1:
        cout << "Monday";
        break;

    case 2:
        cout << "Tuesday";
        break;

    case 3:
        cout << "Wednesday";
        break;

    default:
        cout << "Invalid day";
}
```

Output:

``` text
Tuesday
```

------------------------------------------------------------------------

# 14. How `switch` Works

Suppose:

``` cpp
int choice = 2;
```

Then:

``` text
switch(choice)
      ↓
choice = 2
      ↓
case 1? → No
      ↓
case 2? → YES
      ↓
execute case 2
      ↓
break
      ↓
exit switch
```

------------------------------------------------------------------------

# 15. `case`

A `case` specifies a possible value of the switch expression.

Example:

``` cpp
switch(choice) {

    case 1:
        cout << "Option 1";
        break;

    case 2:
        cout << "Option 2";
        break;
}
```

If:

``` text
choice = 2
```

then:

``` text
case 2
```

matches.

------------------------------------------------------------------------

# 16. `default`

`default` executes when no case matches.

Example:

``` cpp
int choice = 10;

switch(choice) {

    case 1:
        cout << "One";
        break;

    case 2:
        cout << "Two";
        break;

    default:
        cout << "Invalid choice";
}
```

Output:

``` text
Invalid choice
```

### Important

`default` is optional.

It is often useful for handling unexpected values.

------------------------------------------------------------------------

# 17. `break` in `switch`

This is one of the most important `switch` concepts.

Consider:

``` cpp
int x = 1;

switch(x) {

    case 1:
        cout << "A";

    case 2:
        cout << "B";

    case 3:
        cout << "C";
}
```

Output:

``` text
ABC
```

Why?

Because there is no `break`.

This behavior is called **fall-through**.

------------------------------------------------------------------------

# 18. Fall-Through

Normally:

``` cpp
case 1:
    cout << "A";
    break;
```

means:

``` text
execute case 1
      ↓
break
      ↓
exit switch
```

Without `break`:

``` text
case 1
 ↓
execute
 ↓
case 2
 ↓
execute
 ↓
case 3
 ↓
execute
```

### Normal usage

``` cpp
switch(x) {

    case 1:
        cout << "A";
        break;

    case 2:
        cout << "B";
        break;

    case 3:
        cout << "C";
        break;
}
```

------------------------------------------------------------------------

# 19. Intentional Fall-Through

Fall-through can be useful.

Example:

``` cpp
char ch = 'a';

switch(ch) {

    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
        cout << "Vowel";
        break;

    default:
        cout << "Consonant";
}
```

Here multiple cases intentionally share the same code.

``` text
a ─┐
e ─┤
i ─┤
o ─┤ → Vowel
u ─┘
```

------------------------------------------------------------------------

# 20. `if-else` vs `switch`

  `if-else`                             `switch`
  ------------------------------------- ---------------------------------
  Best for conditions and ranges        Best for discrete choices
  Supports `<`, `>`, `&&`, `||`, etc.   Matches against case values
  Can naturally handle ranges           Not naturally suited for ranges
  More flexible                         Often cleaner for menus/options
  Good for complex conditions           Good for fixed choices

### Example suited for `if`

``` cpp
if (marks >= 90)
```

This is a range condition.

### Example suited for `switch`

``` cpp
switch(choice) {
    case 1:
    case 2:
    case 3:
}
```

This is selection among discrete values.

------------------------------------------------------------------------

# 21. Can `switch` Replace Every `if-else`?

**No.**

For example:

``` cpp
if (age >= 18) {
    cout << "Adult";
}
```

is naturally expressed with `if`.

`switch` is designed around matching an expression against case labels,
not arbitrary relational conditions.

Do not force `switch` into situations where `if` is clearer.

------------------------------------------------------------------------

# 22. Ternary Operator `?:`

## Definition

The **conditional operator**, also called the **ternary operator**,
evaluates one of two expressions depending on a condition.

### Syntax

``` cpp
condition ? expression1 : expression2;
```

Meaning:

``` text
condition true
      ↓
expression1

condition false
      ↓
expression2
```

------------------------------------------------------------------------

# 23. Basic Ternary Example

``` cpp
int age = 20;

string result = (age >= 18) ? "Adult" : "Minor";
```

Since:

``` text
20 >= 18 → true
```

we get:

``` text
result = "Adult"
```

------------------------------------------------------------------------

# 24. Ternary vs `if-else`

### `if-else`

``` cpp
if (age >= 18) {
    result = "Adult";
}
else {
    result = "Minor";
}
```

### Ternary

``` cpp
result = (age >= 18) ? "Adult" : "Minor";
```

Use ternary when the logic is **simple and produces a value**.

Avoid deeply nested ternary expressions because they reduce readability.

------------------------------------------------------------------------

# 25. Ternary Is an Expression

The ternary operator produces a value.

Example:

``` cpp
int maximum = (a > b) ? a : b;
```

This is why it can be directly assigned to a variable.

------------------------------------------------------------------------

# 26. Finding Maximum of Two Numbers

``` cpp
int a = 10;
int b = 20;

int maximum = (a > b) ? a : b;

cout << maximum;
```

Output:

``` text
20
```

This pattern appears frequently in DSA.

------------------------------------------------------------------------

# 27. `break`

## Definition

`break` terminates the nearest enclosing loop or `switch`.

Example:

``` cpp
for (int i = 1; i <= 10; i++) {

    if (i == 5) {
        break;
    }

    cout << i << " ";
}
```

Output:

``` text
1 2 3 4
```

### Meaning

``` text
break
  ↓
stop loop completely
```

It does **not** mean "skip this iteration."

------------------------------------------------------------------------

# 28. `continue`

## Definition

`continue` skips the remaining statements of the current loop iteration
and proceeds to the next iteration.

Example:

``` cpp
for (int i = 1; i <= 5; i++) {

    if (i == 3) {
        continue;
    }

    cout << i << " ";
}
```

Output:

``` text
1 2 4 5
```

### Meaning

``` text
continue
   ↓
skip current iteration
   ↓
go to next iteration
```

### Important correction

`continue` must be used within an iteration statement such as:

-   `for`
-   `while`
-   `do-while`

It cannot be used as an independent statement outside a loop.

------------------------------------------------------------------------

# 29. `break` vs `continue`

Memorize this:

``` text
BREAK
 ↓
Terminate the loop/switch

CONTINUE
 ↓
Skip current loop iteration
 ↓
Continue with next iteration
```

Example:

``` cpp
for (int i = 1; i <= 5; i++) {

    if (i == 3)
        continue;

    cout << i << " ";
}
```

Output:

``` text
1 2 4 5
```

But:

``` cpp
for (int i = 1; i <= 5; i++) {

    if (i == 3)
        break;

    cout << i << " ";
}
```

Output:

``` text
1 2
```

------------------------------------------------------------------------

# 30. `return`

## Definition

`return` exits a function and can optionally provide a value to the
caller.

Example:

``` cpp
int add(int a, int b) {
    return a + b;
}
```

Then:

``` cpp
int result = add(10, 20);
```

gives:

``` text
30
```

In:

``` cpp
int main() {
    return 0;
}
```

`return 0` indicates successful termination to the environment.

------------------------------------------------------------------------

# 31. `goto`

## Definition

`goto` transfers execution to a labeled statement.

Example:

``` cpp
goto start;

cout << "This is skipped";

start:
cout << "Hello";
```

Output:

``` text
Hello
```

### Should you use `goto` in DSA?

Generally, **no**.

Prefer structured control flow:

-   `if`
-   loops
-   functions
-   `break`
-   `continue`
-   `return`

because these are easier to understand and maintain.

------------------------------------------------------------------------

# 32. `try-catch` and `throw`

These belong to **exception handling**, not ordinary conditional
statements.

Example:

``` cpp
try {
    throw runtime_error("Something went wrong");
}
catch (const exception& e) {
    cout << e.what();
}
```

Conceptually:

``` text
try
 ↓
exception occurs
 ↓
throw
 ↓
matching catch
 ↓
handle exception
```

For normal beginner DSA problems, exception handling is usually not a
major focus.

------------------------------------------------------------------------

# 33. `switch`, `case`, and `default` Relationship

Think of them like this:

``` text
switch
  │
  ├── case
  │
  ├── case
  │
  └── default
```

A `case` label belongs to a `switch`.

A `default` label belongs to a `switch`.

Example:

``` cpp
switch(x) {

    case 1:
        cout << "One";
        break;

    case 2:
        cout << "Two";
        break;

    default:
        cout << "Other";
}
```

------------------------------------------------------------------------

# 34. ASCII

## Definition

**ASCII** stands for:

> American Standard Code for Information Interchange.

ASCII assigns numeric codes to common characters.

  Character     ASCII
  ----------- -------
  `'0'`            48
  `'1'`            49
  `'9'`            57
  `'A'`            65
  `'B'`            66
  `'Z'`            90
  `'a'`            97
  `'b'`            98
  `'z'`           122
  `' '`            32
  `'\n'`           10
  `'\t'`            9
  `'\r'`           13
  `'\b'`            8
  `'\0'`            0

------------------------------------------------------------------------

# 35. Character to Integer Conversion

A character can be converted to its integer character code.

Example:

``` cpp
char ch = 'A';

cout << static_cast<int>(ch);
```

Output:

``` text
65
```

Similarly:

``` cpp
char ch = 'a';

cout << static_cast<int>(ch);
```

Output:

``` text
97
```

------------------------------------------------------------------------

# 36. Integer to Character

The reverse is also possible:

``` cpp
int x = 65;

cout << static_cast<char>(x);
```

Output:

``` text
A
```

Conceptually:

``` text
65 → 'A'
```

------------------------------------------------------------------------

# 37. Character Arithmetic

This is very useful in DSA.

``` cpp
char ch = 'A';

char next = ch + 1;

cout << next;
```

Output:

``` text
B
```

Conceptually:

``` text
'A' → 65
65 + 1 → 66
66 → 'B'
```

This is useful for character and string problems.

------------------------------------------------------------------------

# 38. Checking Uppercase Character

ASCII uppercase letters are:

``` text
'A' → 65
'Z' → 90
```

Therefore:

``` cpp
if (ch >= 'A' && ch <= 'Z') {
    cout << "Uppercase";
}
```

This is a common DSA/string technique.

------------------------------------------------------------------------

# 39. Checking Lowercase Character

Lowercase letters:

``` text
'a' → 97
'z' → 122
```

So:

``` cpp
if (ch >= 'a' && ch <= 'z') {
    cout << "Lowercase";
}
```

------------------------------------------------------------------------

# 40. Checking Digit Character

Digits:

``` text
'0' → 48
'9' → 57
```

Therefore:

``` cpp
if (ch >= '0' && ch <= '9') {
    cout << "Digit";
}
```

### Very important

Do not confuse:

``` cpp
'5'
```

with:

``` cpp
5
```

They are different.

``` text
'5' → character
5   → integer
```

------------------------------------------------------------------------

# 41. `'0'` vs `'\0'`

This is one of the most important character concepts.

They are completely different.

### `'0'`

Character zero:

``` text
ASCII = 48
```

### `'\0'`

Null character:

``` text
value = 0
```

Therefore:

``` text
'0' != '\0'
```

Remember this carefully.

------------------------------------------------------------------------

# 42. `'\n'`

`\n` represents a newline character.

Example:

``` cpp
cout << "Hello\nWorld";
```

Output:

``` text
Hello
World
```

Common ASCII value:

``` text
'\n' = 10
```

### Important correction

`\n` does **not** mean:

-   end of a string
-   end of a file
-   end of a program
-   end of a function
-   end of a class

It simply represents a **newline character**.

------------------------------------------------------------------------

# 43. `'\0'` in C-Style Strings

For a C-style character array:

``` cpp
char name[] = "Ravi";
```

Conceptually, memory contains:

``` text
R   a   v   i   \0
```

The `'\0'` is the **null character** marking the end of the C-style
string.

This becomes extremely important when studying:

-   character arrays
-   strings
-   pointers
-   memory
-   C-style string algorithms

------------------------------------------------------------------------

# 44. `'\t'`

`\t` represents horizontal tab.

Example:

``` cpp
cout << "Name\tAge";
```

Common ASCII value:

``` text
9
```

------------------------------------------------------------------------

# 45. `'\r'`

`\r` represents **carriage return**.

ASCII value:

``` text
13
```

Historically, it moves the cursor to the beginning of the current line.

Newline conventions differ by operating system:

``` text
Unix/Linux/macOS → \n
Windows           → \r\n
```

------------------------------------------------------------------------

# 46. `'\b'`

`\b` represents backspace.

ASCII value:

``` text
8
```

------------------------------------------------------------------------

# 47. ASCII vs Unicode

### ASCII

A character encoding covering a limited set of common characters.

### Unicode

A much larger character system designed to represent characters from
many writing systems.

For basic DSA problems involving English letters and digits, ASCII
relationships are commonly useful:

``` text
'A' to 'Z'
'a' to 'z'
'0' to '9'
```

------------------------------------------------------------------------

# 48. `if-else` vs `switch` vs Ternary

  -----------------------------------------------------------------------
  Feature           `if-else`         `switch`          Ternary
  ----------------- ----------------- ----------------- -----------------
  Main purpose      General           Match discrete    Simple
                    conditions        values            conditional
                                                        expression

  Range conditions  ✅                ❌ Not naturally  ✅

  Complex           ✅                Limited           Possible, but
  conditions                                            avoid complexity

  Multiple choices  ✅                ✅                ❌ Best for
                                                        simple two-way
                                                        choice

  Produces a value  Not inherently    Not inherently    ✅
  directly                                              

  Readability       High              High for menus    High for simple
                                                        cases

  DSA usage         ⭐⭐⭐⭐⭐        ⭐⭐⭐            ⭐⭐⭐
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 49. Common Beginner Mistakes

## Mistake 1 --- `=` vs `==`

Wrong when comparison is intended:

``` cpp
if (x = 10)
```

Correct:

``` cpp
if (x == 10)
```

------------------------------------------------------------------------

## Mistake 2 --- Wrong range expression

Incorrect:

``` cpp
if (x >= 10 && <= 20)
```

Correct:

``` cpp
if (x >= 10 && x <= 20)
```

------------------------------------------------------------------------

## Mistake 3 --- Incorrect OR condition

Incorrect:

``` cpp
if (x == 1 || 2)
```

Correct:

``` cpp
if (x == 1 || x == 2)
```

------------------------------------------------------------------------

## Mistake 4 --- Forgetting `break`

``` cpp
switch(x) {
    case 1:
        cout << "One";

    case 2:
        cout << "Two";
}
```

This may execute both cases because of fall-through.

------------------------------------------------------------------------

## Mistake 5 --- Confusing `break` and `continue`

``` text
break    → stop loop
continue → skip current iteration
```

------------------------------------------------------------------------

## Mistake 6 --- Confusing `'5'` and `5`

``` text
'5' → character
5   → integer
```

------------------------------------------------------------------------

## Mistake 7 --- Confusing `'0'` and `'\0'`

``` text
'0'  → character zero → ASCII 48
'\0' → null character → value 0
```

------------------------------------------------------------------------

## Mistake 8 --- Incorrect understanding of `\n`

``` text
\n → newline
```

It does not mark the end of a string.

For C-style strings:

``` text
\0 → null terminator
```

------------------------------------------------------------------------

# 50. DSA Pattern: Conditional Filtering

Suppose:

``` cpp
int arr[] = {10, 25, 30, 45, 50};
```

Print only even numbers:

``` cpp
for (int i = 0; i < 5; i++) {

    if (arr[i] % 2 == 0) {
        cout << arr[i] << " ";
    }
}
```

Output:

``` text
10 30 50
```

Conceptually:

``` text
array
  ↓
loop
  ↓
condition
  ↓
modulus
  ↓
comparison
  ↓
output
```

This pattern appears constantly in DSA.

------------------------------------------------------------------------

# 51. DSA Pattern: Find Maximum

``` cpp
int arr[] = {10, 40, 20, 80, 30};

int maximum = arr[0];

for (int i = 1; i < 5; i++) {

    if (arr[i] > maximum) {
        maximum = arr[i];
    }
}

cout << maximum;
```

Output:

``` text
80
```

The key decision is:

``` cpp
if (arr[i] > maximum)
```

This simple pattern becomes the foundation for many array problems.

------------------------------------------------------------------------

# 52. DSA Pattern: Character Classification

``` cpp
char ch;

cin >> ch;

if (ch >= 'A' && ch <= 'Z') {
    cout << "Uppercase";
}
else if (ch >= 'a' && ch <= 'z') {
    cout << "Lowercase";
}
else if (ch >= '0' && ch <= '9') {
    cout << "Digit";
}
else {
    cout << "Special character";
}
```

This combines:

-   input
-   character data
-   ASCII ranges
-   relational operators
-   `if`
-   `else if`
-   `else`

------------------------------------------------------------------------

# 53. Important Mental Models

## `if`

``` text
If condition is true
       ↓
execute block
```

## `if-else`

``` text
condition
 /      \
true    false
 ↓        ↓
if      else
```

## `else-if`

``` text
condition 1?
 ↓
condition 2?
 ↓
condition 3?
 ↓
else
```

## `switch`

``` text
expression
    ↓
case 1?
case 2?
case 3?
    ↓
default
```

## Ternary

``` text
condition ? true_value : false_value
```

## `break`

``` text
EXIT
```

## `continue`

``` text
SKIP CURRENT ITERATION
```

## `return`

``` text
EXIT FUNCTION
```

------------------------------------------------------------------------

# 54. Quick Revision Sheet

### Conditional Statements

``` cpp
if
if-else
else if
nested if
switch-case
```

### Conditional Operator

``` cpp
condition ? expression1 : expression2;
```

### Loop Control

``` cpp
break
continue
```

### Function Control

``` cpp
return
```

### Exception Handling

``` cpp
try
catch
throw
```

### Character Ranges

``` text
'0' → 48
'9' → 57

'A' → 65
'Z' → 90

'a' → 97
'z' → 122
```

### Escape Characters

``` text
\n → newline
\t → horizontal tab
\r → carriage return
\b → backspace
\0 → null character
```

------------------------------------------------------------------------

# 55. Final Comparison

  Construct           Purpose
  ------------------- -----------------------------------------------------------
  `if`                Execute code when condition is true
  `else`              Execute alternative when previous `if` condition is false
  `else if`           Test additional conditions
  Nested `if`         Put one decision inside another
  `switch`            Select based on a discrete expression value
  `case`              Specify a possible switch value
  `default`           Handle unmatched switch values
  `break`             Exit nearest loop/switch
  `continue`          Skip current loop iteration
  `return`            Exit a function and optionally return a value
  `goto`              Jump to a label
  `?:`                Simple conditional expression
  `try/catch/throw`   Exception handling

------------------------------------------------------------------------

# 56. What You Must Master Before Moving to DSA

Make sure these are completely clear:

``` text
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
Data Structures
    ↓
Algorithms
```

Especially master:

``` text
if / else
else-if
switch
ternary
break
continue
integer vs character
ASCII
'\n' vs '\0'
'0' vs 0
'0' vs '\0'
&& vs &
|| vs |
== vs =
```

These concepts will repeatedly appear in:

-   Arrays
-   Searching
-   Sorting
-   Linked Lists
-   Stacks
-   Queues
-   Trees
-   Graphs
-   Recursion
-   Dynamic Programming
-   Bit Manipulation
-   Competitive Programming
