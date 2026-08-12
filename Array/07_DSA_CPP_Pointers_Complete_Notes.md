# 📘 DSA / C++ Complete Notes: Pointers

> **Goal:** Build a strong, confusion-free understanding of C++ pointers from the basics to DSA-level usage.

---

# 1. What Is a Pointer?

A **pointer is a variable that stores the memory address of another variable**.

Example:

```cpp
int a = 12;
int *ptr = &a;
```

Here:

```text
a      → stores the value 12
ptr    → stores the address of a
```

So:

```text
a  = value
ptr = address
```

### Core Definition

> A pointer is a variable whose value is the memory address of another object.

---

# 2. Why Do We Need Pointers?

Pointers are important because they allow us to:

- access memory directly
- modify another variable through its address
- pass variables efficiently to functions
- dynamically allocate memory
- build linked lists
- build trees
- build graphs
- implement dynamic data structures
- work with arrays and strings
- use dynamic memory
- understand references and memory management
- implement many DSA structures

Pointers are especially important in:

```text
Linked List
Tree
Graph
Dynamic Memory
Stack / Queue implementations
Hash tables
Function arguments
```

---

# 3. Memory Basics

Suppose:

```cpp
int a = 12;
```

Conceptually, memory may look like:

```text
Address        Value
1000           12
```

The exact address is determined by the system and may differ every time.

If:

```cpp
int *ptr = &a;
```

then:

```text
ptr
 ↓
1000
```

and:

```text
1000
 ↓
12
```

So:

```text
ptr stores address of a
```

---

# 4. Address-of Operator `&`

The operator:

```cpp
&
```

is called the **address-of operator** when used before a variable.

Example:

```cpp
int a = 12;

cout << &a;
```

This prints the memory address of `a`.

Example output might look like:

```text
0x7ffd1234abcd
```

The exact address is not predictable and can change between executions.

---

# 5. Pointer Declaration

Syntax:

```cpp
dataType *pointerName;
```

Examples:

```cpp
int *ptr;
float *ptr;
char *ptr;
double *ptr;
```

The pointer type should generally correspond to the type of object it points to.

Example:

```cpp
int a = 12;
int *ptr = &a;
```

---

# 6. Important Syntax Understanding

These are equivalent declarations:

```cpp
int* ptr;
```

and:

```cpp
int *ptr;
```

The `*` belongs syntactically to the declarator.

This becomes important when declaring multiple variables:

```cpp
int *p, q;
```

This means:

```text
p → pointer to int
q → ordinary int
```

It does **not** mean both are pointers.

If both should be pointers:

```cpp
int *p, *q;
```

### Recommendation

Prefer:

```cpp
int *ptr;
```

or declare pointers separately for clarity.

---

# 7. Dereference Operator `*`

The `*` operator has another important meaning.

When used with a pointer expression, it is the **dereference operator**.

Example:

```cpp
int a = 12;
int *ptr = &a;

cout << *ptr;
```

Output:

```text
12
```

Why?

Because:

```text
ptr  → address of a
*ptr → value stored at that address
```

---

# 8. `&` vs `*`

This is one of the most important concepts.

```cpp
int a = 12;
int *ptr = &a;
```

### `&a`

Means:

```text
Address of a
```

### `ptr`

Means:

```text
Address stored inside ptr
```

### `*ptr`

Means:

```text
Value located at the address stored in ptr
```

Therefore:

```text
&a  → address
ptr → address
*ptr → value
```

---

# 9. Basic Example

```cpp
#include <iostream>
using namespace std;

int main() {

    int a = 12;

    int *ptr = &a;

    cout << a << endl;
    cout << &a << endl;
    cout << ptr << endl;
    cout << *ptr << endl;

    return 0;
}
```

Conceptually:

```text
a       = 12
&a      = address of a
ptr     = address of a
*ptr    = 12
```

Therefore:

```text
ptr == &a
*ptr == a
```

for this valid pointer setup.

---

# 10. Pointer Diagram

Suppose:

```cpp
int a = 12;
int *ptr = &a;
```

Conceptually:

```text
       a
   ┌─────────┐
   │   12    │
   └─────────┘
       ↑
       │
       │ address
   ┌─────────┐
   │   ptr   │
   └─────────┘
```

More precisely:

```text
ptr ───────────────► a
                     12
```

The arrow represents:

```text
ptr contains the address of a
```

---

# 11. Modifying a Variable Through a Pointer

This is one of the most useful properties of pointers.

```cpp
int a = 12;

int *ptr = &a;

*ptr = 50;
```

Now:

```text
a = 50
```

Why?

Because:

```text
*ptr
```

refers to the actual object stored at that address.

So:

```cpp
*ptr = 50;
```

means:

> Go to the memory location pointed to by `ptr` and store `50` there.

---

# 12. Example

```cpp
int a = 12;

int *ptr = &a;

cout << a << endl;

*ptr = 100;

cout << a << endl;
```

Output:

```text
12
100
```

The pointer modified `a`.

---

# 13. Pointer and Variable Are Different

Suppose:

```cpp
int a = 12;
int *ptr = &a;
```

These are different objects:

```text
a
ptr
```

`a` stores:

```text
12
```

`ptr` stores:

```text
address of a
```

Therefore:

```text
a ≠ ptr
```

But:

```text
*ptr == a
```

---

# 14. Pointer Size

A common misconception:

> "An `int*` is the same size as an `int`."

Not necessarily.

A pointer stores an address, so its size is generally determined by the platform's address representation.

On a typical 64-bit system:

```text
int     → commonly 4 bytes
int*    → commonly 8 bytes
double* → commonly 8 bytes
char*   → commonly 8 bytes
```

You can check:

```cpp
cout << sizeof(int) << endl;
cout << sizeof(int*) << endl;
cout << sizeof(double*) << endl;
```

The exact sizes are implementation-dependent.

---

# 15. Pointer Type Matters

Consider:

```cpp
int a = 10;
int *ptr = &a;
```

`ptr` is:

```text
pointer to int
```

This tells C++:

- what type of object is expected at the pointed address
- how dereferencing should interpret the memory
- how pointer arithmetic should work

---

# 16. Null Pointer

A pointer should not be left uninitialized.

Bad:

```cpp
int *ptr;
```

`ptr` contains an indeterminate value.

Using it before assigning a valid address can cause undefined behavior.

Prefer:

```cpp
int *ptr = nullptr;
```

`nullptr` means:

> This pointer currently points to no object.

Example:

```cpp
int *ptr = nullptr;
```

You can test:

```cpp
if(ptr == nullptr) {
    cout << "Pointer is null";
}
```

---

# 17. `nullptr` vs `NULL`

Modern C++:

```cpp
nullptr
```

is preferred.

Older code may use:

```cpp
NULL
```

or:

```cpp
0
```

Use:

```cpp
nullptr
```

in modern C++.

---

# 18. Dereferencing `nullptr`

This is dangerous:

```cpp
int *ptr = nullptr;

cout << *ptr;
```

There is no valid object at the address represented by `nullptr`.

Dereferencing it causes **undefined behavior**.

### Rule

```text
Never dereference a null pointer.
```

Check first when necessary:

```cpp
if(ptr != nullptr) {
    cout << *ptr;
}
```

---

# 19. Dangling Pointer

A **dangling pointer** is a pointer that refers to an object whose lifetime has ended.

Example:

```cpp
int *ptr;

{
    int a = 10;
    ptr = &a;
}

// a no longer exists here
```

Now:

```cpp
ptr
```

is dangling.

Do not dereference it.

---

# 20. Wild Pointer

A **wild pointer** is an uninitialized pointer.

Example:

```cpp
int *ptr;
```

Before assigning a valid address, `ptr` contains an indeterminate value.

Bad:

```cpp
cout << *ptr;
```

Better:

```cpp
int *ptr = nullptr;
```

---

# 21. Void Pointer

A `void*` is a pointer that can hold the address of an object of any object type.

Example:

```cpp
int a = 10;

void *ptr = &a;
```

However, you cannot directly dereference a `void*` because it does not specify the pointed-to type.

You need to convert it:

```cpp
cout << *static_cast<int*>(ptr);
```

For normal C++ programming, prefer typed pointers when possible.

---

# 22. Pointer to Pointer

A pointer can store the address of another pointer.

Example:

```cpp
int a = 12;

int *ptr = &a;

int **ptr2 = &ptr;
```

Now we have three levels:

```text
a
ptr
ptr2
```

---

# 23. Understanding `int **`

```cpp
int **ptr2;
```

means:

```text
ptr2 is a pointer to a pointer to an int
```

Not:

```text
ptr2 is an integer
```

The levels are:

```text
int
 ↓
int*
 ↓
int**
```

---

# 24. Pointer-to-Pointer Diagram

Given:

```cpp
int a = 12;
int *ptr = &a;
int **ptr2 = &ptr;
```

Conceptually:

```text
ptr2
  │
  ▼
 ptr
  │
  ▼
  a
  │
  ▼
 12
```

Therefore:

```text
ptr2  → ptr
ptr   → a
```

---

# 25. Dereferencing Multiple Levels

Given:

```cpp
int a = 12;
int *ptr = &a;
int **ptr2 = &ptr;
```

Then:

```cpp
*ptr2
```

gives:

```text
ptr
```

And:

```cpp
**ptr2
```

gives:

```text
a
```

Therefore:

```text
ptr2   → address of ptr
*ptr2  → ptr
**ptr2 → value of a
```

---

# 26. Three Levels of Pointers

You can technically have:

```cpp
int ***ptr3;
```

Example:

```cpp
int a = 12;

int *p = &a;
int **pp = &p;
int ***ppp = &pp;
```

Then:

```text
***ppp
```

gives:

```text
12
```

Conceptually:

```text
ppp
 ↓
pp
 ↓
p
 ↓
a
 ↓
12
```

Multiple levels are possible, although excessive indirection can make code harder to understand.

---

# 27. Modifying Through Pointer-to-Pointer

Example:

```cpp
int a = 12;

int *ptr = &a;

int **ptr2 = &ptr;

**ptr2 = 100;
```

Now:

```text
a = 100
```

because:

```text
ptr2
 ↓
ptr
 ↓
a
```

and:

```text
**ptr2
```

reaches `a`.

---

# 28. Pointer Arithmetic

Pointers support arithmetic when they point into an array or one-past its end.

Example:

```cpp
int arr[] = {10,20,30,40};

int *ptr = arr;
```

Initially:

```text
ptr → arr[0]
```

Then:

```cpp
ptr++;
```

Now:

```text
ptr → arr[1]
```

Another:

```cpp
ptr++;
```

Now:

```text
ptr → arr[2]
```

---

# 29. Important Pointer Arithmetic Rule

If:

```cpp
int *ptr;
```

then:

```cpp
ptr + 1
```

does **not** necessarily mean:

```text
address + 1 byte
```

It means:

> Move to the next `int` object.

If `sizeof(int) == 4`, the underlying byte address typically changes by 4 bytes.

Example conceptually:

```text
1000 → arr[0]
1004 → arr[1]
1008 → arr[2]
1012 → arr[3]
```

But actual addresses depend on the implementation.

---

# 30. Pointer Arithmetic With Arrays

```cpp
int arr[] = {10,20,30,40};

int *ptr = arr;

cout << *ptr << endl;       // 10
cout << *(ptr + 1) << endl; // 20
cout << *(ptr + 2) << endl; // 30
cout << *(ptr + 3) << endl; // 40
```

This is a fundamental relationship:

```text
arr[i] == *(arr + i)
```

---

# 31. Array Name and Pointer

For most expressions, an array name can decay into a pointer to its first element.

Example:

```cpp
int arr[] = {10,20,30};

int *ptr = arr;
```

This is equivalent to:

```cpp
int *ptr = &arr[0];
```

Therefore:

```text
arr → address of first element in many expressions
```

But an array is **not itself a pointer**.

This distinction is very important.

---

# 32. Array vs Pointer

```cpp
int arr[5];
int *ptr = arr;
```

They are not the same type.

```text
arr → array of 5 int
ptr → pointer to int
```

For example:

```cpp
sizeof(arr)
```

returns the size of the entire array when `arr` is an actual array in that scope.

But:

```cpp
sizeof(ptr)
```

returns the size of the pointer.

This is one of the easiest ways to see that arrays and pointers are different.

---

# 33. Pointer Increment

Example:

```cpp
int arr[] = {10,20,30};

int *ptr = arr;

cout << *ptr << endl;

ptr++;

cout << *ptr << endl;
```

Output:

```text
10
20
```

Pointer increment changes which array element it points to.

It does not modify the array element itself.

---

# 34. Pointer Decrement

```cpp
ptr--;
```

moves the pointer to the previous element.

Example:

```text
arr[0] ← arr[1] ← arr[2]
```

If:

```text
ptr → arr[2]
```

then:

```cpp
ptr--;
```

gives:

```text
ptr → arr[1]
```

---

# 35. Pointer + Integer

```cpp
ptr + 3
```

means:

> Move three elements forward.

Example:

```cpp
int arr[] = {10,20,30,40,50};

int *ptr = arr;

cout << *(ptr + 3);
```

Output:

```text
40
```

---

# 36. Pointer - Integer

```cpp
ptr - 2
```

means:

> Move two elements backward.

Example:

```cpp
int *ptr = &arr[4];

cout << *(ptr - 2);
```

This accesses:

```text
arr[2]
```

---

# 37. Pointer Difference

If two pointers point into the same array, subtracting them gives the number of elements between them.

Example:

```cpp
int arr[] = {10,20,30,40,50};

int *p = &arr[1];
int *q = &arr[4];

cout << q - p;
```

Output:

```text
3
```

Because:

```text
arr[4] - arr[1]
```

represents three element positions.

---

# 38. Comparing Pointers

Pointers can be compared.

For pointers into the same array, relational comparisons can be used meaningfully:

```cpp
p < q
p > q
p <= q
p >= q
```

Equality comparisons are also common:

```cpp
p == q
p != q
```

For example:

```cpp
if(ptr == nullptr) {
}
```

---

# 39. One-Past-the-End Pointer

For an array:

```cpp
int arr[5];
```

the pointer:

```cpp
arr + 5
```

is allowed as a pointer value for one-past-the-end.

But:

```cpp
*(arr + 5)
```

is invalid because there is no element at index `5`.

This is why loops often use:

```cpp
for(int *p = arr; p != arr + 5; p++) {
    cout << *p;
}
```

---

# 40. Pointer Traversal of an Array

```cpp
int arr[] = {10,20,30,40};

int *ptr = arr;

for(int i = 0; i < 4; i++) {
    cout << *(ptr + i) << " ";
}
```

Output:

```text
10 20 30 40
```

Another form:

```cpp
for(int *p = arr; p != arr + 4; p++) {
    cout << *p << " ";
}
```

---

# 41. Pointers and Functions

Pointers allow a function to modify the caller's object.

Example:

```cpp
void change(int *ptr) {
    *ptr = 100;
}

int main() {

    int a = 10;

    change(&a);

    cout << a;
}
```

Output:

```text
100
```

---

# 42. Pass by Value vs Pointer

## Pass by Value

```cpp
void change(int x) {
    x = 100;
}
```

Calling:

```cpp
int a = 10;
change(a);
```

does not change `a`.

Why?

A copy is passed.

---

## Pass by Pointer

```cpp
void change(int *x) {
    *x = 100;
}
```

Call:

```cpp
change(&a);
```

Now the original `a` changes.

---

# 43. Pass by Reference vs Pointer

C++ also has references.

### Pointer

```cpp
void change(int *x) {
    *x = 100;
}

change(&a);
```

### Reference

```cpp
void change(int &x) {
    x = 100;
}

change(a);
```

Both can modify the original object.

### Major difference

A pointer:

```text
can be nullptr
can be reassigned
requires dereferencing to access the pointed object
```

A reference:

```text
must be bound to an object when initialized
cannot be null in normal use
cannot be reseated to refer to another object
is used like the referred object
```

---

# 44. Pointer Reassignment

A pointer can point to different objects.

```cpp
int a = 10;
int b = 20;

int *ptr = &a;

cout << *ptr; // 10

ptr = &b;

cout << *ptr; // 20
```

The pointer changed what it points to.

The variables themselves did not move.

---

# 45. Pointer vs Changing the Pointed Value

These are different:

```cpp
*ptr = 50;
```

and:

```cpp
ptr = &b;
```

### `*ptr = 50`

Changes the value of the object being pointed to.

### `ptr = &b`

Changes which object the pointer points to.

This distinction is critical.

---

# 46. Pointer to Constant

```cpp
const int a = 10;

const int *ptr = &a;
```

This means:

> Pointer to a const int.

You cannot modify the object through `ptr`:

```cpp
*ptr = 20; // ERROR
```

But the pointer itself can be changed:

```cpp
int b = 30;

ptr = &b;
```

---

# 47. Constant Pointer

```cpp
int a = 10;

int *const ptr = &a;
```

This means:

> `ptr` itself cannot be changed to point somewhere else.

This is invalid:

```cpp
int b = 20;

ptr = &b; // ERROR
```

But the pointed value can be modified:

```cpp
*ptr = 50;
```

---

# 48. Constant Pointer to Constant

```cpp
const int a = 10;

const int *const ptr = &a;
```

Now:

```text
The pointer cannot change.
The pointed value cannot be changed through the pointer.
```

Therefore neither is allowed:

```cpp
ptr = &b;  // ERROR
*ptr = 20; // ERROR
```

---

# 49. Easy Way to Read `const` Pointer Declarations

### `const int *p`

Read:

> Pointer to const int.

```text
value cannot be changed through p
p can change
```

### `int *const p`

Read:

> Const pointer to int.

```text
p cannot change
value can change
```

### `const int *const p`

Read:

> Const pointer to const int.

```text
p cannot change
value cannot change through p
```

---

# 50. Dynamic Memory Allocation

Pointers become especially important when memory is allocated dynamically.

Modern C++ generally prefers:

```text
std::vector
std::string
smart pointers
RAII
```

over raw `new`/`delete` for most application code.

However, understanding raw dynamic memory is important for DSA and interviews.

---

# 51. `new`

Example:

```cpp
int *ptr = new int;
```

This dynamically allocates an `int`.

We can initialize it:

```cpp
int *ptr = new int(10);
```

Now:

```cpp
cout << *ptr;
```

prints:

```text
10
```

---

# 52. `delete`

Memory allocated using:

```cpp
new
```

must eventually be released using:

```cpp
delete
```

Example:

```cpp
int *ptr = new int(10);

cout << *ptr;

delete ptr;

ptr = nullptr;
```

After deletion, do not dereference `ptr`.

---

# 53. Dynamic Array

Allocate:

```cpp
int *arr = new int[5];
```

Use:

```cpp
arr[0] = 10;
arr[1] = 20;
```

Release:

```cpp
delete[] arr;
```

### Important

For:

```cpp
new int
```

use:

```cpp
delete
```

For:

```cpp
new int[5]
```

use:

```cpp
delete[]
```

Do not mix them.

---

# 54. Memory Leak

A memory leak occurs when dynamically allocated memory is no longer reachable but has not been released.

Example:

```cpp
int *ptr = new int(10);

ptr = nullptr;
```

The allocated memory is now lost.

There is no pointer through which it can be deleted.

That memory is leaked.

Correct:

```cpp
int *ptr = new int(10);

delete ptr;
ptr = nullptr;
```

---

# 55. Use-After-Free

Example:

```cpp
int *ptr = new int(10);

delete ptr;

cout << *ptr;
```

This is invalid.

After:

```cpp
delete ptr;
```

the object no longer exists.

A useful defensive pattern is:

```cpp
delete ptr;
ptr = nullptr;
```

Then:

```cpp
if(ptr != nullptr) {
    cout << *ptr;
}
```

---

# 56. Double Delete

This is also invalid:

```cpp
int *ptr = new int(10);

delete ptr;
delete ptr;
```

The second deletion attempts to release an already-deleted object.

Safer:

```cpp
delete ptr;
ptr = nullptr;
```

Then:

```cpp
delete ptr;
```

is harmless because deleting a null pointer is permitted.

Still, ownership should be designed clearly rather than relying on this.

---

# 57. Smart Pointers

Modern C++ provides smart pointers:

```cpp
unique_ptr
shared_ptr
weak_ptr
```

They manage dynamic lifetime automatically.

Example:

```cpp
#include <memory>

unique_ptr<int> ptr = make_unique<int>(10);
```

No explicit:

```cpp
delete
```

is needed.

For modern C++, prefer RAII and smart pointers when dynamic ownership is actually required.

---

# 58. Pointer and Linked List

Pointers are fundamental to linked lists.

Example node:

```cpp
struct Node {
    int data;
    Node* next;
};
```

Here:

```text
data → stores value
next → stores address of another Node
```

Example:

```text
10 → 20 → 30 → nullptr
```

Conceptually:

```text
┌───────┬──────┐
│  10   │  ─────────► Node 20
└───────┴──────┘
```

This is one of the most important DSA applications of pointers.

---

# 59. Creating a Linked List Node

```cpp
Node* newNode = new Node;

newNode->data = 10;
newNode->next = nullptr;
```

Notice:

```cpp
newNode->data
```

instead of:

```cpp
(*newNode).data
```

These are equivalent:

```cpp
newNode->data
```

and:

```cpp
(*newNode).data
```

---

# 60. Arrow Operator `->`

The arrow operator is used when accessing a member through a pointer to an object.

If:

```cpp
Node *ptr;
```

then:

```cpp
ptr->data
```

means:

```cpp
(*ptr).data
```

### Rule

```text
object:
    object.member

pointer:
    pointer->member
```

Example:

```cpp
Node node;

node.data = 10;
```

Pointer:

```cpp
Node *ptr = &node;

ptr->data = 20;
```

---

# 61. `.` vs `->`

| Situation | Operator |
|---|---|
| Object | `.` |
| Pointer to object | `->` |

Example:

```cpp
Node n;

n.data = 10;
```

Pointer:

```cpp
Node *p = &n;

p->data = 20;
```

Equivalent:

```cpp
(*p).data = 20;
```

---

# 62. Pointers in Trees

A binary tree node commonly looks like:

```cpp
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
};
```

Conceptually:

```text
          10
         /  \
        5    20
       / \
      2   7
```

The pointers connect nodes:

```text
left  → left child
right → right child
```

If there is no child:

```cpp
left = nullptr;
```

or:

```cpp
right = nullptr;
```

---

# 63. Pointers in Graphs

Graphs can also use pointers.

For example, adjacency structures may contain:

```text
nodes
edges
linked structures
dynamic objects
```

Pointers allow one object to reference another.

However, modern C++ graph implementations often use:

```cpp
vector<vector<int>>
```

or other containers instead of raw pointers.

---

# 64. Double Pointers in DSA

Pointer-to-pointer is especially useful when a function needs to modify a pointer itself.

Example:

```cpp
void changePointer(int **p) {

    static int x = 100;

    *p = &x;
}
```

Caller:

```cpp
int *ptr = nullptr;

changePointer(&ptr);
```

Now `ptr` points to `x`.

This concept appears in linked-list operations such as modifying the head pointer.

---

# 65. Why `Node**` Can Be Useful in Linked Lists

Suppose:

```cpp
Node* head;
```

If a function needs to change:

```cpp
head
```

it can receive:

```cpp
Node** head
```

Example:

```cpp
void insertAtBeginning(Node** head, int value);
```

The function can then modify:

```cpp
*head
```

Modern C++ often provides cleaner alternatives using:

```cpp
Node*& head
```

or returning the new head, but understanding `Node**` is important.

---

# 66. Pointer to Function

Pointers can also point to functions.

Example:

```cpp
int add(int a, int b) {
    return a + b;
}

int (*ptr)(int, int) = add;
```

Call:

```cpp
cout << ptr(2,3);
```

Output:

```text
5
```

This is called a **function pointer**.

---

# 67. Function Pointer Syntax

General form:

```cpp
returnType (*pointerName)(parameterTypes);
```

Example:

```cpp
int (*ptr)(int, int);
```

means:

> `ptr` is a pointer to a function taking two `int`s and returning an `int`.

Function pointers are useful for:

- callbacks
- generic algorithms
- event systems
- low-level programming

Modern C++ often uses lambdas and `std::function` where appropriate.

---

# 68. Pointer to Pointer vs Reference

Consider:

```cpp
int *ptr;
```

and:

```cpp
int &ref;
```

A pointer:

```text
stores an address
can be null
can be reassigned
supports pointer arithmetic in applicable cases
```

A reference:

```text
aliases an existing object
normally must be initialized
cannot be null in normal language semantics
cannot be reseated
```

Example:

```cpp
int a = 10;
int b = 20;

int *p = &a;
p = &b;
```

Pointer now refers to `b`.

Reference:

```cpp
int &r = a;
```

You cannot make `r` start referring to `b` by assignment:

```cpp
r = b;
```

This assigns `b`'s value to `a`; it does not reseat the reference.

---

# 69. Pointers and `const` in Function Parameters

Suppose:

```cpp
void print(const int *ptr) {
    cout << *ptr;
}
```

The function promises not to modify the pointed value through `ptr`.

This is useful when passing arrays or objects that should not be modified.

Example:

```cpp
void printArray(const int *arr, int n) {

    for(int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}
```

---

# 70. Passing Arrays to Functions

```cpp
void printArray(int *arr, int n) {

    for(int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}
```

Call:

```cpp
int arr[] = {10,20,30};

printArray(arr, 3);
```

The array name decays to a pointer to its first element.

Modern C++ alternatives include:

```cpp
std::span
std::array
std::vector
```

depending on the problem.

---

# 71. Important Array-Pointer Confusion

Inside:

```cpp
void printArray(int *arr)
```

you cannot determine the original array length using:

```cpp
sizeof(arr)
```

because `arr` is a pointer parameter.

Example:

```cpp
void func(int arr[]) {
    cout << sizeof(arr);
}
```

Here the parameter is adjusted to a pointer type.

Therefore, pass the size separately:

```cpp
void func(int *arr, int n)
```

or use modern containers such as:

```cpp
vector<int>
array<int, N>
span<int>
```

---

# 72. Pointer and String Literals

C-style strings use arrays of characters:

```cpp
char str[] = "Hello";
```

The array contains:

```text
H e l l o \0
```

A pointer can point to its first character:

```cpp
char *ptr = str;
```

Then:

```cpp
cout << ptr;
```

prints the C-string until the null terminator.

---

# 73. `char*` and String Literals

Be careful with:

```cpp
char *p = "Hello";
```

In modern C++, string literals are not modifiable and this should not be used as a mutable `char*`.

Prefer:

```cpp
const char *p = "Hello";
```

or:

```cpp
string s = "Hello";
```

for modern C++.

---

# 74. Pointers and Memory Layout

A useful mental model:

```text
Stack
----------------
local variables
----------------

Heap
----------------
dynamically allocated objects
----------------

Code / Static storage
----------------
program code / global and static objects
----------------
```

Pointers can point to objects in different storage areas, but the lifetime and validity rules matter.

Do not assume every pointer points to the heap.

For example:

```cpp
int a = 10;
int *p = &a;
```

`a` is typically an automatic local variable, not a heap allocation.

---

# 75. Stack vs Heap

## Stack / Automatic Storage

```cpp
int a = 10;
```

The object has automatic storage duration.

Its lifetime is generally tied to the scope in which it is created.

## Dynamic Storage

```cpp
int *p = new int(10);
```

The object has dynamic storage duration.

Its lifetime continues until released, or until ownership is managed by an appropriate RAII mechanism.

---

# 76. Pointer Lifetime Rule

A pointer is valid only when:

1. It contains an appropriate address.
2. The pointed object is still alive.
3. The access is permitted by the language rules.
4. The pointer has not been invalidated by an operation that changes the object's storage or lifetime.

This is why dangling pointers are dangerous.

---

# 77. Pointer Invalidation

Some operations can invalidate pointers.

For example, a `vector` may reallocate its storage when it grows.

Example:

```cpp
vector<int> v;

v.push_back(10);

int *p = &v[0];

v.push_back(20);
```

The second `push_back` may cause reallocation.

If reallocation occurs, `p` may no longer point to the valid element.

Therefore, don't assume pointers into containers remain valid after operations that can invalidate them.

---

# 78. `vector` and Pointers

Example:

```cpp
vector<int> v = {10,20,30};

int *p = v.data();
```

Then:

```cpp
cout << *p;
```

prints:

```text
10
```

And:

```cpp
cout << *(p + 1);
```

prints:

```text
20
```

But pointer validity must be considered after vector modifications.

---

# 79. Smart Pointer Overview

### `unique_ptr`

One owner.

```cpp
unique_ptr<Node> ptr;
```

Best when one object has a clear owner.

### `shared_ptr`

Multiple shared owners.

```cpp
shared_ptr<Node> ptr;
```

Uses reference counting.

### `weak_ptr`

Non-owning observer of an object managed by `shared_ptr`.

Useful for avoiding ownership cycles.

---

# 80. Raw Pointer vs Smart Pointer

| Feature | Raw Pointer | Smart Pointer |
|---|---|---|
| Automatic ownership | No | Yes |
| Can be null | Yes | Yes |
| Manual `delete` | If owning | Generally no |
| Ownership semantics | Not expressed | Expressed |
| Modern C++ preference | For non-owning / low-level cases | For owning dynamic objects |

For DSA interview implementations, raw pointers are still frequently taught because they make the underlying structure explicit.

---

# 81. Pointer Safety Rules

### Rule 1

Initialize pointers:

```cpp
int *p = nullptr;
```

when they don't immediately point to an object.

### Rule 2

Never dereference `nullptr`.

### Rule 3

Don't dereference dangling pointers.

### Rule 4

Don't use uninitialized pointers.

### Rule 5

Don't access outside an array.

### Rule 6

Match:

```text
new       ↔ delete
new[]     ↔ delete[]
```

### Rule 7

Prefer RAII and standard containers in modern C++.

### Rule 8

Understand ownership before using dynamic memory.

---

# 82. Common Pointer Mistakes

## Mistake 1

```cpp
int *ptr;
cout << *ptr;
```

Problem:

```text
Uninitialized pointer
```

---

## Mistake 2

```cpp
int *ptr = nullptr;
cout << *ptr;
```

Problem:

```text
Dereferencing null
```

---

## Mistake 3

```cpp
int *ptr = new int(10);

delete ptr;

cout << *ptr;
```

Problem:

```text
Use-after-free
```

---

## Mistake 4

```cpp
int *ptr = new int[10];

delete ptr;
```

Problem:

```text
Mismatched allocation/deallocation
```

Correct:

```cpp
delete[] ptr;
```

---

## Mistake 5

```cpp
int a = 10;
int *p = &a;

p = nullptr;

cout << *p;
```

Problem:

```text
Null dereference
```

---

## Mistake 6

Confusing:

```cpp
ptr
```

with:

```cpp
*ptr
```

Remember:

```text
ptr  = address
*ptr = value at that address
```

---

# 83. `*p++` vs `(*p)++`

These are different.

## `*p++`

Operator precedence means this is interpreted as:

```cpp
*(p++)
```

So:

```text
Use current pointer value, then increment pointer.
```

## `(*p)++`

Means:

```text
Increment the value pointed to by p.
```

Example:

```cpp
int arr[] = {10,20};
int *p = arr;

(*p)++;
```

Now:

```text
arr = {11,20}
```

But:

```cpp
*p++;
```

moves the pointer.

This is a very common pointer question.

---

# 84. `*p + 1` vs `*(p + 1)`

Also different.

### `*p + 1`

Means:

```text
value pointed to by p + 1
```

### `*(p + 1)`

Means:

```text
value at the next pointer position
```

Example:

```cpp
int arr[] = {10,20,30};

int *p = arr;
```

Then:

```cpp
*p + 1
```

gives:

```text
11
```

while:

```cpp
*(p + 1)
```

gives:

```text
20
```

---

# 85. Operator Precedence Matters

Expressions involving pointers can become confusing.

When unsure, add parentheses.

Instead of:

```cpp
*p++
```

write:

```cpp
*(p++)
```

if that is what you mean.

Instead of:

```cpp
*p + 1
```

use:

```cpp
(*p) + 1
```

for clarity.

---

# 86. Pointer to Struct

Example:

```cpp
struct Student {
    int age;
};

Student s;

Student *ptr = &s;

ptr->age = 20;
```

Equivalent:

```cpp
(*ptr).age = 20;
```

Remember:

```text
`.`  → object
`->` → pointer to object
```

---

# 87. Pointers in Linked List — Basic Example

```cpp
struct Node {
    int data;
    Node* next;

    Node(int value) {
        data = value;
        next = nullptr;
    }
};
```

Create:

```cpp
Node* head = new Node(10);
head->next = new Node(20);
head->next->next = new Node(30);
```

Structure:

```text
head
 ↓
10 → 20 → 30 → nullptr
```

This is the foundation of a singly linked list.

---

# 88. Traversing a Linked List

```cpp
Node* temp = head;

while(temp != nullptr) {

    cout << temp->data << " ";

    temp = temp->next;
}
```

This pattern is extremely important.

### Mental model

```text
temp
 ↓
current node
 ↓
print
 ↓
temp = temp->next
 ↓
next node
```

---

# 89. Pointer as a DSA Tool

Pointers allow us to create relationships:

```text
Node A
   ↓
Node B
   ↓
Node C
```

This is why linked lists, trees, and many graph structures are possible.

Instead of storing all objects contiguously, one object can store a reference/address to another object.

---

# 90. Pointer-Based DSA Structures

Pointers commonly appear in:

```text
Singly Linked List
Doubly Linked List
Circular Linked List
Binary Tree
Binary Search Tree
AVL Tree
Heap implementations
Graph nodes
Trie implementations
Dynamic stacks
Dynamic queues
```

---

# 91. Doubly Linked List

A doubly linked list node typically has:

```cpp
struct Node {
    int data;
    Node* prev;
    Node* next;
};
```

Conceptually:

```text
nullptr ← 10 ⇄ 20 ⇄ 30 → nullptr
```

`prev` points backward.

`next` points forward.

---

# 92. Circular Linked List

A circular list can have:

```text
10 → 20 → 30
↑         ↓
└─────────┘
```

The final node points back to the first node.

Pointers make this possible.

---

# 93. Tree Node

```cpp
struct Node {
    int data;
    Node* left;
    Node* right;
};
```

Conceptually:

```text
          10
         /  \
        5    15
```

The `left` and `right` pointers connect nodes.

---

# 94. Pointer Recursion Connection

Tree algorithms often use pointers:

```cpp
void preorder(Node* root) {

    if(root == nullptr)
        return;

    cout << root->data;

    preorder(root->left);
    preorder(root->right);
}
```

Notice:

```cpp
Node* root
```

and:

```cpp
root->left
root->right
```

Pointers are therefore essential for understanding recursive tree algorithms.

---

# 95. `const` and DSA

A common function:

```cpp
void print(Node* root)
```

If the function should not modify the node through the pointer, you may use:

```cpp
void print(const Node* root)
```

Then:

```cpp
root->data
```

can be read, but modification through `root` is prohibited.

This is useful for expressing intent.

---

# 96. Important Pointer Relationships

Given:

```cpp
int a = 12;
int *ptr = &a;
int **ptr2 = &ptr;
```

Memorize:

```text
&a       → address of a
ptr      → address of a
*ptr     → a's value

&ptr     → address of ptr
ptr2     → address of ptr
*ptr2    → ptr
**ptr2   → a's value
```

---

# 97. Golden Pointer Table

| Expression | Meaning |
|---|---|
| `a` | Value of `a` |
| `&a` | Address of `a` |
| `ptr` | Address stored in `ptr` |
| `*ptr` | Value at address stored in `ptr` |
| `&ptr` | Address of pointer `ptr` |
| `ptr2` | Address stored in `ptr2` |
| `*ptr2` | Pointer `ptr` |
| `**ptr2` | Value of `a` |

---

# 98. Pointer Levels

```text
int a
```

One ordinary integer.

```text
int *p
```

Pointer to integer.

```text
int **pp
```

Pointer to pointer to integer.

```text
int ***ppp
```

Pointer to pointer to pointer to integer.

Think:

```text
***ppp
 ↓
**pp
 ↓
*p
 ↓
value
```

---

# 99. Pointer Questions You Must Be Able to Answer

### Q1
What is a pointer?

**Answer:**

A variable that stores the address of another object.

---

### Q2
What does `&a` mean?

**Answer:**

Address of `a`.

---

### Q3
What does `*ptr` mean?

**Answer:**

The object/value at the address stored in `ptr`.

---

### Q4
What does `int **ptr2` mean?

**Answer:**

A pointer to a pointer to an `int`.

---

### Q5
What does `nullptr` mean?

**Answer:**

A null pointer value that represents no valid pointed-to object.

---

### Q6
Can we dereference `nullptr`?

**Answer:**

No. Doing so is undefined behavior.

---

### Q7
What is a dangling pointer?

**Answer:**

A pointer whose pointed-to object's lifetime has ended or whose target is otherwise no longer valid.

---

### Q8
What is pointer arithmetic?

**Answer:**

Arithmetic on pointers to elements of an array/object sequence, where movement is measured in elements rather than raw bytes.

---

### Q9
What is `ptr + 1`?

**Answer:**

For a pointer into an array, a pointer to the next element.

---

### Q10
What is `arr[i]` equivalent to?

**Answer:**

```cpp
*(arr + i)
```

for ordinary array indexing.

---

# 100. Interview-Level Questions

### Q11
Difference between:

```cpp
int *p;
int **p;
```

### Q12
Difference between:

```cpp
p
*p
&p
```

### Q13
Difference between:

```cpp
*p++
(*p)++
```

### Q14
Difference between:

```cpp
*p + 1
*(p + 1)
```

### Q15
Difference between:

```cpp
.
->
```

### Q16
Difference between:

```cpp
int *p
const int *p
int *const p
const int *const p
```

### Q17
Why is:

```cpp
delete[]
```

used with:

```cpp
new[]
```

### Q18
Why can array pointers become invalid after vector reallocation?

### Q19
Why can a pointer become dangling?

### Q20
Why are pointers important in linked lists?

---

# 101. Pointer Practice Programs

## Program 1 — Print Value Through Pointer

```cpp
#include <iostream>
using namespace std;

int main() {

    int a = 25;

    int *ptr = &a;

    cout << *ptr;

    return 0;
}
```

Expected:

```text
25
```

---

## Program 2 — Modify Through Pointer

```cpp
int a = 10;

int *ptr = &a;

*ptr = 50;

cout << a;
```

Output:

```text
50
```

---

## Program 3 — Pointer to Pointer

```cpp
int a = 10;

int *p = &a;

int **pp = &p;

cout << **pp;
```

Output:

```text
10
```

---

## Program 4 — Array Traversal

```cpp
int arr[] = {10,20,30,40};

int *p = arr;

for(int i = 0; i < 4; i++) {
    cout << *(p + i) << " ";
}
```

Output:

```text
10 20 30 40
```

---

## Program 5 — Swap Using Pointers

```cpp
void swapValues(int *a, int *b) {

    int temp = *a;

    *a = *b;

    *b = temp;
}
```

Usage:

```cpp
int x = 10;
int y = 20;

swapValues(&x, &y);
```

Now:

```text
x = 20
y = 10
```

---

# 102. Swap — Why Pointers Work

Initially:

```text
x = 10
y = 20
```

Pass:

```cpp
&x
&y
```

Function receives their addresses.

Therefore:

```cpp
*a
```

refers to `x`.

And:

```cpp
*b
```

refers to `y`.

So:

```cpp
*a = *b;
```

can directly modify the caller's variables.

---

# 103. Pointer Mindset

When looking at pointer code, always ask three questions:

### Question 1

**What is stored in the pointer?**

```text
Address
```

### Question 2

**What object does that address belong to?**

```text
int?
Node?
TreeNode?
Array element?
```

### Question 3

**What happens when I dereference it?**

```text
*ptr
```

means:

```text
Access the pointed-to object.
```

This mental process removes most pointer confusion.

---

# 104. ⭐ Pointer Master Mental Model

Given:

```cpp
int a = 12;
int *ptr = &a;
int **ptr2 = &ptr;
```

Visualize:

```text
              stores 12
        ┌─────────────────┐
        │       a         │
        │       12        │
        └─────────────────┘
                ▲
                │
             address
                │
        ┌─────────────────┐
        │      ptr        │
        │   address of a  │
        └─────────────────┘
                ▲
                │
             address
                │
        ┌─────────────────┐
        │     ptr2        │
        │  address of ptr │
        └─────────────────┘
```

Therefore:

```text
ptr2
 ↓
ptr
 ↓
a
 ↓
12
```

And:

```text
ptr2   → address of ptr
*ptr2  → ptr
**ptr2 → 12
```

---

# 105. Pointer Complexity

Pointer operations such as:

```cpp
*p
p = &x
p++
```

are generally:

```text
O(1)
```

assuming the operation itself is valid.

Example:

```cpp
cout << *ptr;
```

is constant-time access.

However, traversing `n` pointer-connected nodes:

```cpp
while(ptr != nullptr) {
    ptr = ptr->next;
}
```

takes:

```text
O(n)
```

because we visit `n` nodes.

---

# 106. Pointer vs Dynamic Array

A pointer itself is not automatically dynamic memory.

This:

```cpp
int *p;
```

does not allocate an integer.

This:

```cpp
int *p = &a;
```

points to an existing object.

This:

```cpp
int *p = new int(10);
```

allocates a new integer dynamically.

### Very Important

```text
Pointer ≠ Dynamic Memory
```

A pointer is simply an object that can store an address.

---

# 107. Pointer vs Reference — Final Comparison

| Feature | Pointer | Reference |
|---|---|---|
| Stores address | Yes | Conceptually aliases object |
| Can be null | Yes | No normal null reference |
| Can be reassigned | Yes | No reseating |
| Dereference required | Usually | No |
| Pointer arithmetic | Yes, where valid | No |
| Can point to different objects | Yes | No reseating |
| Common use | Dynamic structures, optional objects, low-level APIs | Function parameters, aliases |
| Syntax | `*p` | `ref` |

---

# 108. The Most Important Rules to Memorize

```text
1. Pointer stores an address.

2. &variable gives the address.

3. *pointer accesses the pointed object.

4. nullptr means no valid object is being pointed to.

5. Never dereference nullptr.

6. Never use an uninitialized pointer.

7. Never dereference a dangling pointer.

8. new → delete

9. new[] → delete[]

10. arr[i] == *(arr + i)

11. . is for objects.

12. -> is for pointers to objects.

13. int** means pointer to pointer.

14. Pointer arithmetic moves by elements for array pointers.

15. Pointer ≠ dynamic memory.

16. Modern C++ prefers RAII and standard containers for ownership.
```

---

# 109. ⭐ Final Pointer Cheat Sheet

```text
POINTER
↓
Variable storing an address
```

### Basic

```cpp
int a = 12;

int *ptr = &a;
```

```text
a      → 12
&a     → address of a
ptr    → address of a
*ptr   → 12
```

### Pointer to Pointer

```cpp
int **ptr2 = &ptr;
```

```text
ptr2   → ptr
*ptr2  → ptr
**ptr2 → a's value
```

### Null

```cpp
int *ptr = nullptr;
```

Never:

```cpp
*ptr
```

when `ptr == nullptr`.

### Array

```cpp
int arr[] = {10,20,30};

int *p = arr;
```

```text
arr[i] == *(arr + i)
```

### Object

```cpp
Node *p;
```

Use:

```cpp
p->data
```

instead of:

```cpp
(*p).data
```

### Dynamic Memory

```cpp
int *p = new int(10);

delete p;
p = nullptr;
```

Array:

```cpp
int *arr = new int[5];

delete[] arr;
arr = nullptr;
```

### Complexity

```text
Direct pointer access → O(1)

Traversing n linked nodes → O(n)
```

---

# 🧠 Final Understanding Test

If you truly understand pointers, you should be able to explain this without memorizing:

```cpp
int a = 12;

int *ptr = &a;

int **ptr2 = &ptr;

**ptr2 = 50;
```

Step by step:

```text
a = 12

ptr = address of a

ptr2 = address of ptr

*ptr2 = ptr

**ptr2 = a

**ptr2 = 50

therefore:

a = 50
```

### The ultimate mental model

```text
Address
   ↓
Pointer
   ↓
Dereference
   ↓
Object
   ↓
Value
```

For multiple pointers:

```text
int
 ↓
int*
 ↓
int**
 ↓
int***
```

Each additional `*` represents another level of indirection.

> **Master this concept and linked lists, trees, dynamic memory, and many pointer-based DSA problems become significantly easier to understand.**
