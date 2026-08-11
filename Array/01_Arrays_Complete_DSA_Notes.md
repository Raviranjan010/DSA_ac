# Arrays in C++ — Complete DSA Notes

> Detailed notes based on the uploaded array material, expanded with additional concepts, examples, edge cases, mistakes, patterns, and practice questions.

---

# 1. What is an Array?

## Definition

An **array** is a collection of elements of the **same type** stored in a fixed-size contiguous block of memory.

Example:

```cpp
int arr[5] = {10, 20, 30, 40, 50};
```

Conceptually:

```text
Index:    0    1    2    3    4
          ↓    ↓    ↓    ↓    ↓
Array:   [10] [20] [30] [40] [50]
```

The first element is at index `0`.

```text
arr[0] → 10
arr[1] → 20
arr[2] → 30
arr[3] → 40
arr[4] → 50
```

The uploaded notes correctly identify zero-based indexing and show basic input/output, minimum, maximum, searching, reversing, and function-based array operations.

---

# 2. Homogeneous Nature of Arrays

A normal C++ array stores elements of one element type.

```cpp
int arr[4] = {10, 20, 30, 40};
```

All elements are `int`.

Similarly:

```cpp
double prices[3] = {10.5, 20.5, 30.5};
```

All elements are `double`.

```cpp
char letters[3] = {'A', 'B', 'C'};
```

All elements are `char`.

### Important correction

The statement:

> "An array having different types of data is called a heterogeneous array."

is not the normal definition of a built-in C++ array.

A standard C++ array is **homogeneous**.

If you need different types together, consider:

- `struct`
- `class`
- `std::tuple`
- `std::variant`

---

# 3. Why Do We Need Arrays?

Without an array:

```cpp
int marks1 = 80;
int marks2 = 75;
int marks3 = 90;
int marks4 = 65;
int marks5 = 88;
```

With an array:

```cpp
int marks[5] = {80, 75, 90, 65, 88};
```

Now we can process all values using a loop:

```cpp
for (int i = 0; i < 5; i++) {
    cout << marks[i] << " ";
}
```

This is one of the biggest advantages of arrays:

> **They allow many related values to be stored and processed using one name and an index.**

---

# 4. Array Indexing

C++ arrays use **zero-based indexing**.

For:

```cpp
int arr[5];
```

valid indices are:

```text
0
1
2
3
4
```

General rule:

```text
valid index = 0 to n - 1
```

where `n` is the array size.

### Example

```cpp
int arr[5] = {10, 20, 30, 40, 50};

cout << arr[0]; // 10
cout << arr[4]; // 50
```

---

# 5. Why Does Indexing Start at 0?

Arrays are stored contiguously.

If the starting address is represented as `base`, the address of an element can be calculated conceptually as:

```text
address(arr[i]) = base + i × sizeof(element)
```

For example, if an `int` occupies 4 bytes:

```text
arr[0] → base
arr[1] → base + 4
arr[2] → base + 8
arr[3] → base + 12
```

The index represents an **offset from the first element**.

This is one reason zero-based indexing fits naturally with memory addressing.

---

# 6. Array Declaration

### Syntax

```cpp
data_type array_name[size];
```

Example:

```cpp
int arr[5];
```

This creates an array capable of storing 5 integers.

---

# 7. Array Initialization

## Method 1 — Full initialization

```cpp
int arr[5] = {10, 20, 30, 40, 50};
```

## Method 2 — Size inferred

```cpp
int arr[] = {10, 20, 30, 40, 50};
```

C++ determines the size as `5`.

## Method 3 — Partial initialization

```cpp
int arr[5] = {10, 20};
```

The remaining elements are initialized to zero:

```text
10 20 0 0 0
```

---

# 8. Array Size

For a built-in array:

```cpp
int arr[] = {10, 20, 30, 40, 50};
```

you can calculate the number of elements using:

```cpp
int n = sizeof(arr) / sizeof(arr[0]);
```

If `int` is 4 bytes:

```text
sizeof(arr)    = 20
sizeof(arr[0]) = 4

20 / 4 = 5
```

Therefore:

```cpp
n = 5;
```

### Important

This works when `arr` is actually an array in that scope.

It does **not** work the same way after an array has decayed to a pointer when passed to a normal function parameter.

---

# 9. Input into an Array

A common pattern:

```cpp
int n;
cin >> n;

int arr[n];

for (int i = 0; i < n; i++) {
    cin >> arr[i];
}
```

### Important C++ note

`int arr[n];` where `n` is determined at runtime is a **variable-length array (VLA)**. It is not part of standard C++.

Some compilers accept it as an extension, but portable C++ should use:

```cpp
vector<int> arr(n);
```

For beginner DSA on platforms that specifically permit VLAs, you may see the original form, but understand the standard C++ distinction.

---

# 10. Printing an Array

```cpp
for (int i = 0; i < n; i++) {
    cout << arr[i] << " ";
}
```

Example:

```text
10 20 30 40 50
```

---

# 11. Traversal

## Definition

**Array traversal** means visiting each element of an array, usually from the first element to the last.

Example:

```cpp
for (int i = 0; i < n; i++) {
    cout << arr[i] << " ";
}
```

### Complexity

```text
Time  = O(n)
Space = O(1)
```

assuming no additional array is created.

---

# 12. Forward Traversal

```cpp
for (int i = 0; i < n; i++) {
    cout << arr[i] << " ";
}
```

Traversal:

```text
0 → 1 → 2 → 3 → ... → n-1
```

---

# 13. Reverse Traversal

```cpp
for (int i = n - 1; i >= 0; i--) {
    cout << arr[i] << " ";
}
```

Traversal:

```text
n-1 → n-2 → ... → 2 → 1 → 0
```

---

# 14. Accessing an Element

Array access:

```cpp
arr[index]
```

Example:

```cpp
int arr[] = {10, 20, 30};

cout << arr[1];
```

Output:

```text
20
```

Access by index is:

```text
Time = O(1)
```

because the address can be calculated directly.

---

# 15. Updating an Element

```cpp
int arr[] = {10, 20, 30};

arr[1] = 100;
```

Array becomes:

```text
10 100 30
```

Complexity:

```text
O(1)
```

---

# 16. Searching in an Array

Searching means finding whether a target value exists and, often, finding its index.

There are two major approaches:

```text
Linear Search
Binary Search
```

---

# 17. Linear Search

## Definition

**Linear search** checks elements sequentially until the target is found or the array ends.

Example:

```cpp
int linearSearch(int arr[], int n, int target) {

    for (int i = 0; i < n; i++) {

        if (arr[i] == target) {
            return i;
        }
    }

    return -1;
}
```

Example:

```text
Array:   10  20  30  40  50
Index:    0   1   2   3   4

Target = 40
```

Checks:

```text
10 → no
20 → no
30 → no
40 → yes
```

Returns:

```text
3
```

---

# 18. Why Return `-1`?

Array indices are normally:

```text
0 to n-1
```

So `-1` cannot be a valid index.

Therefore it is commonly used as a sentinel value meaning:

> Target was not found.

Example:

```cpp
int index = linearSearch(arr, n, target);

if (index == -1) {
    cout << "Not found";
}
else {
    cout << "Found at index " << index;
}
```

---

# 19. Linear Search Complexity

### Best case

Target is at index `0`.

```text
O(1)
```

### Worst case

Target is at the end or absent.

```text
O(n)
```

### Average case

```text
O(n)
```

### Space

```text
O(1)
```

---

# 20. Binary Search

## Definition

**Binary search** repeatedly divides the search range into two halves.

### Critical requirement

The array must be **sorted** according to the ordering being searched.

Example:

```text
1 3 5 7 9 11 13
```

Search for:

```text
9
```

Instead of checking every element, binary search checks the middle and eliminates half of the remaining search space.

---

# 21. Binary Search Dry Run

Array:

```text
1 3 5 7 9 11 13
```

Target:

```text
9
```

Initial:

```text
low = 0
high = 6
mid = 3
```

```text
arr[mid] = 7
```

Since:

```text
9 > 7
```

ignore the left half.

Now:

```text
low = 4
high = 6
```

Middle:

```text
arr[5] = 11
```

Since:

```text
9 < 11
```

search left.

Now:

```text
low = 4
high = 4
```

`arr[4] = 9`

Found.

---

# 22. Binary Search Complexity

```text
Best case  = O(1)
Worst case = O(log n)
Average    = O(log n)
Space      = O(1) for iterative implementation
```

---

# 23. Linear Search vs Binary Search

| Feature | Linear Search | Binary Search |
|---|---|---|
| Requires sorted array? | No | Yes |
| Approach | Sequential | Divide and conquer |
| Worst-case | O(n) | O(log n) |
| Easy to implement | Yes | Moderate |
| Works on unsorted array | Yes | No |
| Good for small arrays | Yes | Yes |
| Good for large sorted arrays | Sometimes | Excellent |

---

# 24. Minimum Element

A common array problem is finding the smallest element.

### Approach

Start with the first element:

```cpp
int smallest = arr[0];
```

Then compare every element:

```cpp
for (int i = 1; i < n; i++) {

    if (arr[i] < smallest) {
        smallest = arr[i];
    }
}
```

### Why start with `arr[0]`?

Because it guarantees that the initial value actually belongs to the array.

---

# 25. Using `INT_MAX`

Another approach:

```cpp
int smallest = INT_MAX;

for (int i = 0; i < n; i++) {
    if (arr[i] < smallest) {
        smallest = arr[i];
    }
}
```

`INT_MAX` is larger than every representable `int` value.

Therefore the first array element will replace it.

### Header

Use:

```cpp
#include <climits>
```

for `INT_MAX` and `INT_MIN`.

### Preferred beginner approach

```cpp
int smallest = arr[0];
```

is often simpler and also handles the important idea that the array must be non-empty.

---

# 26. Maximum Element

```cpp
int largest = arr[0];

for (int i = 1; i < n; i++) {

    if (arr[i] > largest) {
        largest = arr[i];
    }
}
```

Complexity:

```text
Time  = O(n)
Space = O(1)
```

---

# 27. `INT_MIN` and `INT_MAX`

You can use:

```cpp
INT_MIN
```

as an initial value for maximum.

And:

```cpp
INT_MAX
```

as an initial value for minimum.

Example:

```cpp
int largest = INT_MIN;
int smallest = INT_MAX;
```

But for a non-empty array, this is often simpler:

```cpp
int largest = arr[0];
int smallest = arr[0];
```

---

# 28. Sum of Array Elements

### Problem

Find the sum of all elements.

```cpp
int sum = 0;

for (int i = 0; i < n; i++) {
    sum += arr[i];
}

cout << sum;
```

Example:

```text
Array: 1 2 3 4 5

sum = 1 + 2 + 3 + 4 + 5
    = 15
```

### Complexity

```text
Time  = O(n)
Space = O(1)
```

---

# 29. Product of Array Elements

```cpp
long long product = 1;

for (int i = 0; i < n; i++) {
    product *= arr[i];
}
```

### Why `1`?

Because `1` is the multiplicative identity:

```text
1 × x = x
```

Starting with `0` would make the entire product zero.

### Important

Use a sufficiently large integer type if the product can exceed `int`.

Even `long long` can overflow for sufficiently large products.

---

# 30. Count Even and Odd Elements

```cpp
int even = 0;
int odd = 0;

for (int i = 0; i < n; i++) {

    if (arr[i] % 2 == 0)
        even++;
    else
        odd++;
}
```

---

# 31. Count Positive, Negative, and Zero

```cpp
int positive = 0;
int negative = 0;
int zero = 0;

for (int i = 0; i < n; i++) {

    if (arr[i] > 0)
        positive++;
    else if (arr[i] < 0)
        negative++;
    else
        zero++;
}
```

---

# 32. Reverse an Array

## Definition

Reversing an array means changing:

```text
1 2 3 4 5
```

into:

```text
5 4 3 2 1
```

The uploaded material uses the correct **two-pointer/in-place** approach.

---

# 33. Two-Pointer Reverse

```cpp
void reverseArr(int arr[], int n) {

    int start = 0;
    int end = n - 1;

    while (start < end) {

        swap(arr[start], arr[end]);

        start++;
        end--;
    }
}
```

### Dry Run

Array:

```text
1 2 3 4 5
```

Initial:

```text
start = 0
end   = 4
```

Swap:

```text
5 2 3 4 1
```

Move:

```text
start = 1
end = 3
```

Swap:

```text
5 4 3 2 1
```

Move:

```text
start = 2
end = 2
```

Stop.

---

# 34. Why `start < end`?

We only need to swap pairs until the pointers meet.

If:

```text
start == end
```

there is a single middle element, which does not need swapping.

Therefore:

```cpp
while (start < end)
```

is the correct condition.

---

# 35. Reverse Complexity

```text
Time  = O(n)
Space = O(1)
```

It is an **in-place** reversal because no second array is created.

---

# 36. Swapping Maximum and Minimum

### Problem

Given:

```text
5 2 9 1 7
```

minimum:

```text
1
```

maximum:

```text
9
```

After swapping their positions:

```text
5 2 1 9 7
```

### Approach

1. Find minimum value and its index.
2. Find maximum value and its index.
3. Swap the two positions.

```cpp
int minIndex = 0;
int maxIndex = 0;

for (int i = 1; i < n; i++) {

    if (arr[i] < arr[minIndex])
        minIndex = i;

    if (arr[i] > arr[maxIndex])
        maxIndex = i;
}

swap(arr[minIndex], arr[maxIndex]);
```

### Complexity

```text
Time  = O(n)
Space = O(1)
```

---

# 37. Important Question: What If Minimum = Maximum?

Example:

```text
5 5 5 5
```

Both minimum and maximum are `5`.

Swapping their positions changes nothing.

Result:

```text
5 5 5 5
```

This is an important edge case.

---

# 38. Unique Elements

## What Does "Unique" Mean?

There are two common interpretations.

### Interpretation 1

Print elements that appear **exactly once**.

Example:

```text
Input:
1 2 2 3 4 4 5

Output:
1 3 5
```

### Interpretation 2

Print each distinct value only once.

Example:

```text
Input:
1 2 2 3 4 4 5

Output:
1 2 3 4 5
```

These are **different problems**.

Always determine which meaning the question intends.

---

# 39. Print Elements Appearing Exactly Once

Simple approach using nested loops:

```cpp
for (int i = 0; i < n; i++) {

    int count = 0;

    for (int j = 0; j < n; j++) {

        if (arr[i] == arr[j]) {
            count++;
        }
    }

    if (count == 1) {
        cout << arr[i] << " ";
    }
}
```

Complexity:

```text
Time  = O(n²)
Space = O(1)
```

---

# 40. Distinct Elements Using `set`

If you want each value only once:

```cpp
set<int> s;

for (int i = 0; i < n; i++) {
    s.insert(arr[i]);
}
```

Then:

```cpp
for (int x : s) {
    cout << x << " ";
}
```

Note:

> `set` stores unique values and keeps them ordered.

If you need insertion-order-like behavior or faster average lookup, other approaches may be appropriate.

---

# 41. Frequency of an Element

### Problem

Count how many times `target` occurs.

```cpp
int count = 0;

for (int i = 0; i < n; i++) {

    if (arr[i] == target) {
        count++;
    }
}
```

Example:

```text
Array:
1 2 2 3 2 4

target = 2

count = 3
```

---

# 42. First Occurrence

The first occurrence is the smallest index at which the target appears.

```cpp
int index = -1;

for (int i = 0; i < n; i++) {

    if (arr[i] == target) {
        index = i;
        break;
    }
}
```

---

# 43. Last Occurrence

```cpp
int index = -1;

for (int i = 0; i < n; i++) {

    if (arr[i] == target) {
        index = i;
    }
}
```

Example:

```text
Array: 1 2 3 2 4 2

target = 2
```

Last occurrence:

```text
index = 5
```

---

# 44. Check if Array is Sorted

Suppose:

```text
1 2 3 4 5
```

is sorted in non-decreasing order.

We check adjacent elements.

```cpp
bool sorted = true;

for (int i = 1; i < n; i++) {

    if (arr[i] < arr[i - 1]) {
        sorted = false;
        break;
    }
}
```

If `sorted` remains true, the array is sorted.

### Complexity

```text
O(n)
```

---

# 45. Ascending vs Strictly Increasing

These are different.

### Non-decreasing

```text
1 2 2 3 4
```

Duplicates allowed.

Condition:

```cpp
arr[i] >= arr[i - 1]
```

### Strictly increasing

```text
1 2 3 4 5
```

Duplicates are not allowed.

Condition:

```cpp
arr[i] > arr[i - 1]
```

---

# 46. Copy an Array

```cpp
for (int i = 0; i < n; i++) {
    copy[i] = arr[i];
}
```

Complexity:

```text
Time  = O(n)
Space = O(n)
```

because a second array is created.

---

# 47. In-Place vs Extra-Space Operations

### In-place

Modifies the original array.

Example:

```cpp
swap(arr[i], arr[j]);
```

Extra space:

```text
O(1)
```

### Extra array

Creates another array.

```cpp
int copy[n];
```

Extra space:

```text
O(n)
```

This distinction becomes very important in DSA interviews.

---

# 48. Passing Arrays to Functions

Example:

```cpp
void printArray(int arr[], int n) {

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}
```

Call:

```cpp
int arr[] = {1, 2, 3, 4, 5};

printArray(arr, 5);
```

### Important correction

It is misleading to simply say:

> "An array is passed by reference."

For a built-in array parameter written as:

```cpp
void func(int arr[], int n)
```

the parameter is adjusted to a pointer type.

Conceptually:

```cpp
void func(int* arr, int n)
```

So the function receives access to the original array elements.

Therefore:

```cpp
arr[i] = 100;
```

inside the function changes the original array.

---

# 49. Modifying an Array in a Function

```cpp
void changeArr(int arr[], int n) {

    for (int i = 0; i < n; i++) {
        arr[i] *= 2;
    }
}
```

Main:

```cpp
int arr[] = {1, 2, 3, 4, 5};

changeArr(arr, 5);
```

Array becomes:

```text
2 4 6 8 10
```

---

# 50. Why Does the Array Change?

Because the function receives access to the same underlying array storage.

Conceptually:

```text
main array
   ↓
[1][2][3][4][5]
   ↑
   |
function accesses same elements
```

So:

```cpp
arr[i] *= 2;
```

modifies the original elements.

---

# 51. `const` Array Parameter

If a function should only read the array and must not modify it:

```cpp
void printArray(const int arr[], int n) {

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}
```

This gives the function a read-only view of the elements.

This is a very good habit for functions that do not need to modify the array.

---

# 52. Array of Characters

An array can store characters:

```cpp
char letters[] = {'A', 'B', 'C'};
```

It can also represent a C-style string:

```cpp
char name[] = "Ravi";
```

The second form contains an additional null terminator:

```text
R a v i \0
```

---

# 53. Two-Dimensional Array

A two-dimensional array is an array arranged in rows and columns.

```cpp
int matrix[3][4];
```

This means:

```text
3 rows
4 columns
```

Conceptually:

```text
[ ][ ][ ][ ]
[ ][ ][ ][ ]
[ ][ ][ ][ ]
```

Access:

```cpp
matrix[row][column]
```

Example:

```cpp
matrix[1][2]
```

means:

```text
row = 1
column = 2
```

---

# 54. Traversing a 2D Array

```cpp
for (int i = 0; i < rows; i++) {

    for (int j = 0; j < cols; j++) {

        cout << matrix[i][j] << " ";
    }

    cout << "\n";
}
```

Complexity:

```text
O(rows × cols)
```

---

# 55. Row Sum

For a matrix:

```cpp
for (int i = 0; i < rows; i++) {

    int sum = 0;

    for (int j = 0; j < cols; j++) {
        sum += matrix[i][j];
    }

    cout << "Row " << i << ": " << sum << "\n";
}
```

---

# 56. Column Sum

```cpp
for (int j = 0; j < cols; j++) {

    int sum = 0;

    for (int i = 0; i < rows; i++) {
        sum += matrix[i][j];
    }

    cout << "Column " << j << ": " << sum << "\n";
}
```

---

# 57. Primary Diagonal

For a square matrix:

```text
1 2 3
4 5 6
7 8 9
```

Primary diagonal:

```text
1
  5
    9
```

Condition:

```cpp
i == j
```

Example:

```cpp
for (int i = 0; i < n; i++) {
    cout << matrix[i][i] << " ";
}
```

Output:

```text
1 5 9
```

---

# 58. Secondary Diagonal

For:

```text
1 2 3
4 5 6
7 8 9
```

Secondary diagonal:

```text
    3
  5
7
```

Condition:

```text
i + j = n - 1
```

Code:

```cpp
for (int i = 0; i < n; i++) {
    cout << matrix[i][n - 1 - i] << " ";
}
```

---

# 59. Array Rotation

Rotation is different from reversal.

### Left rotation by 1

```text
1 2 3 4 5
```

becomes:

```text
2 3 4 5 1
```

### Right rotation by 1

```text
1 2 3 4 5
```

becomes:

```text
5 1 2 3 4
```

Rotation is a very common array interview problem.

---

# 60. Left Rotation by One

Simple approach:

```cpp
int first = arr[0];

for (int i = 0; i < n - 1; i++) {
    arr[i] = arr[i + 1];
}

arr[n - 1] = first;
```

Example:

```text
Before:
1 2 3 4 5

After:
2 3 4 5 1
```

---

# 61. Right Rotation by One

```cpp
int last = arr[n - 1];

for (int i = n - 1; i > 0; i--) {
    arr[i] = arr[i - 1];
}

arr[0] = last;
```

Example:

```text
Before:
1 2 3 4 5

After:
5 1 2 3 4
```

---

# 62. Move Zeros to the End

### Problem

Input:

```text
0 1 0 3 12
```

Output:

```text
1 3 12 0 0
```

A common two-pointer approach:

```cpp
int j = 0;

for (int i = 0; i < n; i++) {

    if (arr[i] != 0) {
        swap(arr[i], arr[j]);
        j++;
    }
}
```

### Complexity

```text
Time  = O(n)
Space = O(1)
```

---

# 63. Find Second Largest Element

Do not simply sort the array unless sorting is actually allowed.

A one-pass approach:

```cpp
long long largest = LLONG_MIN;
long long secondLargest = LLONG_MIN;

for (int i = 0; i < n; i++) {

    if (arr[i] > largest) {
        secondLargest = largest;
        largest = arr[i];
    }
    else if (arr[i] > secondLargest && arr[i] != largest) {
        secondLargest = arr[i];
    }
}
```

### Important

Clarify whether "second largest" means:

- second largest **distinct** value
- second element after sorting, where duplicates may count

These are different problems.

---

# 64. Find Missing Number

Suppose the array contains numbers from:

```text
0 to n
```

with exactly one missing.

Example:

```text
0 1 3 4
```

Missing:

```text
2
```

One mathematical approach:

```cpp
long long expected = 1LL * n * (n + 1) / 2;

long long actual = 0;

for (int x : arr) {
    actual += x;
}

cout << expected - actual;
```

---

# 65. Duplicate Element

Example:

```text
1 3 4 2 2
```

The duplicate is:

```text
2
```

There are multiple approaches depending on constraints:

- nested loops
- sorting
- frequency array
- `set` / `unordered_set`
- Floyd's cycle detection for special problem constraints

Do not automatically choose one method without checking the constraints.

---

# 66. Intersection of Two Arrays

The uploaded file includes this as a practice problem.

Example:

```text
A = 1 2 3 4
B = 3 4 5 6
```

Intersection:

```text
3 4
```

### Important ambiguity

"Intersection" may mean:

1. distinct common values
2. common values respecting duplicates/multiset frequency

Example:

```text
A = 1 2 2 3
B = 2 2 4
```

Distinct intersection:

```text
2
```

Multiset intersection:

```text
2 2
```

Always clarify the intended definition.

---

# 67. Brute-Force Intersection

For distinct values, a simple approach can use nested loops plus duplicate checking.

Basic complexity can be:

```text
O(n × m)
```

where:

- `n` = size of first array
- `m` = size of second array

For larger constraints, hashing or sorting-based solutions are usually better.

---

# 68. Prefix Sum

## Definition

A **prefix sum array** stores cumulative sums.

For:

```text
arr = [2, 4, 1, 3, 5]
```

prefix sums:

```text
[2, 6, 7, 10, 15]
```

Because:

```text
2
2+4 = 6
2+4+1 = 7
2+4+1+3 = 10
2+4+1+3+5 = 15
```

---

# 69. Why Prefix Sum Is Important

Suppose we need many range-sum queries.

For example:

```text
sum from index 1 to 3
```

Without prefix sums, repeatedly summing can take:

```text
O(n)
```

With prefix sums, each range sum can be answered in:

```text
O(1)
```

after:

```text
O(n)
```

preprocessing.

---

# 70. Range Sum Formula

If:

```text
prefix[i] = arr[0] + ... + arr[i]
```

then:

```text
sum(l, r) = prefix[r] - prefix[l - 1]
```

when `l > 0`.

For `l = 0`:

```text
sum(0, r) = prefix[r]
```

A cleaner implementation often uses a prefix array of size `n + 1`:

```cpp
vector<long long> prefix(n + 1, 0);

for (int i = 0; i < n; i++) {
    prefix[i + 1] = prefix[i] + arr[i];
}
```

Then:

```cpp
sum(l, r) = prefix[r + 1] - prefix[l];
```

This avoids a special `l == 0` case.

---

# 71. Kadane's Algorithm — Maximum Subarray Sum

### Problem

Find the maximum sum of a contiguous subarray.

Example:

```text
[-2,1,-3,4,-1,2,1,-5,4]
```

Maximum-sum subarray:

```text
[4,-1,2,1]
```

Sum:

```text
6
```

A common implementation:

```cpp
long long current = arr[0];
long long best = arr[0];

for (int i = 1; i < n; i++) {

    current = max(1LL * arr[i], current + arr[i]);

    best = max(best, current);
}
```

Complexity:

```text
Time  = O(n)
Space = O(1)
```

This is one of the most important array algorithms for interviews.

---

# 72. Subarray vs Subsequence vs Subset

These are commonly confused.

## Subarray

Elements must be **contiguous**.

```text
[2, 3, 4]
```

from:

```text
1 2 3 4 5
```

is a subarray.

## Subsequence

Order is preserved, but elements do not need to be contiguous.

```text
1 3 5
```

is a subsequence of:

```text
1 2 3 4 5
```

## Subset

Order generally does not matter.

For:

```text
{1, 2, 3}
```

possible subsets include:

```text
{}
{1}
{2}
{1,3}
{1,2,3}
```

This distinction becomes very important in DSA.

---

# 73. Time Complexity of Common Array Operations

| Operation | Complexity |
|---|---:|
| Access by index | O(1) |
| Update by index | O(1) |
| Traverse | O(n) |
| Linear search | O(n) |
| Binary search | O(log n), sorted data required |
| Find min/max | O(n) |
| Reverse | O(n) |
| Copy | O(n) |
| Insert at end of fixed array if free position exists | O(1) |
| Insert at beginning | O(n) |
| Insert in middle | O(n) |
| Delete from beginning | O(n) |
| Delete from middle | O(n) |

---

# 74. Why Array Access Is O(1)

Suppose:

```text
arr = [10,20,30,40,50]
```

To access:

```cpp
arr[3]
```

we don't need to inspect:

```text
arr[0]
arr[1]
arr[2]
```

The address is calculated directly from the base address and index.

Therefore:

```text
arr[i] → O(1)
```

This is one of the biggest strengths of arrays.

---

# 75. Why Insertion at the Beginning Is O(n)

Suppose:

```text
10 20 30 40
```

Insert `5` at index `0`.

We must shift:

```text
10 → 1
20 → 2
30 → 3
40 → 4
```

Result:

```text
5 10 20 30 40
```

Potentially many elements must move.

Therefore:

```text
O(n)
```

---

# 76. Array vs Linked List

| Feature | Array | Linked List |
|---|---|---|
| Memory layout | Contiguous | Nodes can be non-contiguous |
| Random access | O(1) | O(n) |
| Search | O(n) generally | O(n) |
| Insert beginning | O(n) | O(1) with head |
| Delete beginning | O(n) | O(1) with head |
| Cache locality | Usually good | Usually weaker |
| Fixed built-in array size | Yes | Dynamic node structure |
| Extra pointer memory | No | Yes |

This comparison becomes important when you study linked lists.

---

# 77. Array vs `vector`

A built-in array:

```cpp
int arr[5];
```

has a fixed size.

A `vector`:

```cpp
vector<int> arr;
```

is a dynamic array abstraction.

Example:

```cpp
vector<int> arr = {1, 2, 3};

arr.push_back(4);
```

Now:

```text
1 2 3 4
```

For modern C++ DSA, `vector` is usually preferred when the size is determined at runtime.

---

# 78. Common Array Mistakes

## Mistake 1 — Out-of-bounds access

For:

```cpp
int arr[5];
```

valid indices:

```text
0,1,2,3,4
```

This is invalid:

```cpp
arr[5]
```

---

## Mistake 2 — Loop boundary error

Wrong:

```cpp
for (int i = 0; i <= n; i++)
```

Correct:

```cpp
for (int i = 0; i < n; i++)
```

Because the last valid index is:

```text
n - 1
```

---

## Mistake 3 — Starting maximum at zero

This fails for an all-negative array.

Example:

```text
-5 -10 -2
```

If:

```cpp
int largest = 0;
```

you may incorrectly get:

```text
0
```

which isn't even in the array.

Prefer:

```cpp
int largest = arr[0];
```

for a non-empty array.

---

## Mistake 4 — Starting product at zero

Wrong:

```cpp
int product = 0;
```

Then:

```text
0 × anything = 0
```

Correct:

```cpp
long long product = 1;
```

---

## Mistake 5 — Binary search on an unsorted array

Binary search requires appropriate sorted ordering.

Do not apply binary search blindly to:

```text
8 2 10 1 5
```

---

## Mistake 6 — Forgetting empty-array cases

Code like:

```cpp
int smallest = arr[0];
```

requires at least one element.

If `n == 0`, there is no `arr[0]`.

Always understand the problem's constraints.

---

## Mistake 7 — Integer overflow

This can overflow:

```cpp
int sum = 0;
```

if the values and `n` are large.

Sometimes use:

```cpp
long long sum = 0;
```

depending on constraints.

---

# 79. Edge Cases You Must Check

Whenever solving an array problem, ask:

### Case 1 — Empty array

```text
[]
```

Is it allowed?

### Case 2 — One element

```text
[5]
```

### Case 3 — All equal

```text
[7,7,7,7]
```

### Case 4 — All negative

```text
[-5,-2,-10]
```

### Case 5 — All positive

```text
[1,5,9]
```

### Case 6 — Duplicate values

```text
[1,2,2,3]
```

### Case 7 — Already sorted

```text
[1,2,3,4,5]
```

### Case 8 — Reverse sorted

```text
[5,4,3,2,1]
```

### Case 9 — Target absent

```text
target = 100
```

### Case 10 — Target occurs multiple times

```text
[2,5,2,7,2]
```

These cases reveal many bugs.

---

# 80. Array Problem-Solving Checklist

Before coding, ask:

```text
1. Is the array sorted?
2. Are duplicates allowed?
3. Do I need the value or index?
4. Do I need first occurrence or last occurrence?
5. Is the answer based on contiguous elements?
6. Is extra space allowed?
7. Can I use hashing?
8. Can I use two pointers?
9. Can I use prefix sums?
10. Can I use binary search?
11. Are negative numbers possible?
12. Can values overflow int?
13. Can n be zero?
14. Is the result required modulo something?
15. What is the expected complexity?
```

---

# 81. Important Array Patterns

You should eventually recognize these patterns:

## Pattern 1 — Simple Traversal

```cpp
for (int i = 0; i < n; i++)
```

Used for:

- sum
- count
- min/max
- search
- frequency

---

## Pattern 2 — Two Pointers

```cpp
int left = 0;
int right = n - 1;
```

Used for:

- reverse
- pair problems
- sorted-array problems
- partitioning
- removing duplicates

---

## Pattern 3 — Sliding Window

Used for:

- subarray problems
- fixed-size windows
- longest/shortest valid ranges

---

## Pattern 4 — Prefix Sum

Used for:

- repeated range-sum queries
- subarray sum calculations
- cumulative information

---

## Pattern 5 — Hashing

Used for:

- frequency
- duplicates
- two-sum type problems
- distinct elements

---

## Pattern 6 — Binary Search

Used when:

- search space is ordered
- answer has a monotonic property
- sorted data is available
- "binary search on answer" is applicable

---

# 82. Practice Questions — Beginner

## Q1. Print all array elements

Input:

```text
5
10 20 30 40 50
```

Output:

```text
10 20 30 40 50
```

---

## Q2. Find the sum

Input:

```text
5
1 2 3 4 5
```

Output:

```text
15
```

---

## Q3. Find minimum

Input:

```text
5
8 3 10 2 6
```

Output:

```text
2
```

---

## Q4. Find maximum

Input:

```text
5
8 3 10 2 6
```

Output:

```text
10
```

---

## Q5. Count even numbers

Input:

```text
6
1 2 4 7 8 9
```

Output:

```text
3
```

---

## Q6. Count positive, negative, and zero

Input:

```text
7
-2 0 5 -1 0 8 3
```

Expected:

```text
Positive = 3
Negative = 2
Zero = 2
```

---

# 83. Practice Questions — Searching

## Q7. Linear search

Find the index of `30`:

```text
10 20 30 40 50
```

Expected:

```text
2
```

---

## Q8. Search for a missing value

```text
Array = 10 20 30 40
Target = 50
```

Expected:

```text
-1
```

---

## Q9. First occurrence

```text
Array = 2 5 2 7 2
Target = 2
```

Expected:

```text
0
```

---

## Q10. Last occurrence

Same array:

```text
2 5 2 7 2
```

Expected:

```text
4
```

---

## Q11. Count occurrences

```text
Array = 1 2 2 3 2 4
Target = 2
```

Expected:

```text
3
```

---

# 84. Practice Questions — Reverse & Manipulation

## Q12. Reverse an array

Input:

```text
1 2 3 4 5
```

Output:

```text
5 4 3 2 1
```

Constraint:

> Do it in-place.

---

## Q13. Swap minimum and maximum

Input:

```text
5 2 9 1 7
```

Output:

```text
5 2 1 9 7
```

---

## Q14. Left rotate by one

Input:

```text
1 2 3 4 5
```

Output:

```text
2 3 4 5 1
```

---

## Q15. Right rotate by one

Input:

```text
1 2 3 4 5
```

Output:

```text
5 1 2 3 4
```

---

# 85. Practice Questions — Duplicates & Uniqueness

## Q16. Print elements occurring exactly once

Input:

```text
1 2 2 3 4 4 5
```

Output:

```text
1 3 5
```

---

## Q17. Print each distinct value once

Input:

```text
1 2 2 3 4 4 5
```

Output:

```text
1 2 3 4 5
```

---

## Q18. Find duplicate values

Input:

```text
1 2 3 2 4 1
```

Expected duplicate values:

```text
1 2
```

---

# 86. Practice Questions — Sorted Arrays

## Q19. Check whether array is sorted

Input:

```text
1 2 3 4 5
```

Output:

```text
Sorted
```

---

## Q20. Check non-decreasing order

Input:

```text
1 2 2 3 4
```

Output:

```text
Sorted
```

---

## Q21. Check strictly increasing order

Input:

```text
1 2 2 3
```

Output:

```text
Not strictly increasing
```

---

# 87. Practice Questions — Intermediate

## Q22. Find second largest distinct element

Input:

```text
10 5 20 8 20
```

Expected:

```text
10
```

---

## Q23. Move all zeros to the end

Input:

```text
0 1 0 3 12
```

Expected:

```text
1 3 12 0 0
```

Try to solve in:

```text
O(n) time
O(1) extra space
```

---

## Q24. Find missing number

Numbers are from `0` to `n`.

Input:

```text
0 1 3 4
```

Expected:

```text
2
```

---

## Q25. Find intersection

```text
A = 1 2 3 4
B = 3 4 5 6
```

Expected:

```text
3 4
```

---

## Q26. Find union of two arrays

```text
A = 1 2 3
B = 2 3 4
```

Distinct union:

```text
1 2 3 4
```

---

# 88. Practice Questions — Prefix Sum

## Q27. Build prefix sum

Input:

```text
2 4 1 3 5
```

Expected:

```text
2 6 7 10 15
```

---

## Q28. Range sum

Array:

```text
2 4 1 3 5
```

Find sum from index `1` to `3`.

Calculation:

```text
4 + 1 + 3 = 8
```

Expected:

```text
8
```

---

# 89. Practice Questions — Two Pointers

## Q29. Reverse in-place

Constraint:

```text
Do not create another array.
```

---

## Q30. Two Sum in Sorted Array

Given:

```text
1 2 4 6 8 9
```

Target:

```text
10
```

Find two elements whose sum is `10`.

Expected pair:

```text
2 + 8
```

A two-pointer approach can solve this in:

```text
O(n)
```

because the array is sorted.

---

# 90. Practice Questions — Subarrays

## Q31. Maximum subarray sum

Input:

```text
-2 1 -3 4 -1 2 1 -5 4
```

Expected:

```text
6
```

---

## Q32. Print all subarrays

Input:

```text
1 2 3
```

Subarrays:

```text
[1]
[1,2]
[1,2,3]
[2]
[2,3]
[3]
```

Number of non-empty subarrays:

```text
n(n+1)/2
```

For `n = 3`:

```text
3 × 4 / 2 = 6
```

---

# 91. Practice Questions — 2D Arrays

## Q33. Print matrix

Input:

```text
1 2 3
4 5 6
7 8 9
```

Output:

```text
1 2 3
4 5 6
7 8 9
```

---

## Q34. Row sums

For:

```text
1 2 3
4 5 6
7 8 9
```

Expected:

```text
6
15
24
```

---

## Q35. Column sums

Expected:

```text
12
15
18
```

---

## Q36. Primary diagonal

Expected:

```text
1 5 9
```

---

## Q37. Secondary diagonal

Expected:

```text
3 5 7
```

---

# 92. Interview-Level Questions

### Q38. Why is array access O(1)?

Explain using:

```text
base address + index × element size
```

---

### Q39. Why does array indexing start at zero?

Explain the index as an offset from the first element.

---

### Q40. Why is insertion at the beginning O(n)?

Explain element shifting.

---

### Q41. Why is binary search O(log n)?

Explain how the search space becomes approximately:

```text
n
n/2
n/4
n/8
...
1
```

---

### Q42. What is the difference between an array and a vector?

Discuss:

- size
- memory
- resizing
- insertion
- C++ usage

---

### Q43. What is array decay?

Explain why:

```cpp
void func(int arr[])
```

behaves like:

```cpp
void func(int* arr)
```

for a function parameter.

---

### Q44. Why can't a function automatically know the length of a raw array parameter?

Because the array parameter is adjusted to a pointer, so the size information is not carried with that parameter.

That's why we commonly pass:

```cpp
func(arr, n);
```

---

### Q45. What happens if we access `arr[n]`?

For an array with `n` elements, `arr[n]` is outside the valid index range.

Accessing it results in **undefined behavior**.

---

# 93. Array Problem Recognition Guide

When you see:

### "Find maximum/minimum"

Think:

```text
single traversal
```

### "Find whether target exists"

Think:

```text
linear search
```

### "Sorted array + search"

Think:

```text
binary search
```

### "Reverse array"

Think:

```text
two pointers
```

### "Pair sum in sorted array"

Think:

```text
two pointers
```

### "Repeated range sums"

Think:

```text
prefix sum
```

### "Frequency / duplicates"

Think:

```text
hashing / frequency array / set
```

### "Contiguous segment"

Think:

```text
subarray
sliding window
prefix sum
Kadane
```

### "Rotate"

Think:

```text
shifting
or
reversal algorithm
```

---

# 94. Most Important Array Concepts to Master

Before moving to advanced DSA, make sure you understand:

```text
1. Array definition
2. Homogeneous storage
3. Contiguous memory
4. Zero-based indexing
5. Declaration
6. Initialization
7. Traversal
8. Access
9. Update
10. Searching
11. Linear search
12. Binary search
13. Minimum
14. Maximum
15. Sum
16. Product
17. Frequency
18. Reverse
19. Two pointers
20. In-place operations
21. Passing arrays to functions
22. const array parameters
23. 2D arrays
24. Row/column traversal
25. Diagonals
26. Rotation
27. Duplicates
28. Unique elements
29. Prefix sums
30. Subarrays
31. Kadane's algorithm
32. Array complexity
33. Edge cases
34. Overflow
35. Array vs vector
36. Array vs linked list
```

---

# 95. Final Array Cheat Sheet

```text
Array
│
├── Same element type
├── Contiguous storage
├── Zero-based indexing
├── Fixed size for built-in array
│
├── Access → O(1)
├── Update → O(1)
├── Traverse → O(n)
├── Search → O(n)
├── Binary Search → O(log n)
├── Reverse → O(n)
├── Min/Max → O(n)
│
├── Patterns
│   ├── Traversal
│   ├── Two pointers
│   ├── Sliding window
│   ├── Prefix sum
│   ├── Hashing
│   └── Binary search
│
└── Important problems
    ├── Sum
    ├── Min/Max
    ├── Search
    ├── Reverse
    ├── Rotate
    ├── Duplicates
    ├── Unique elements
    ├── Intersection
    ├── Missing number
    ├── Second largest
    ├── Move zeros
    ├── Two Sum
    ├── Prefix Sum
    └── Maximum Subarray
```

---

# 96. Recommended Learning Order

Study arrays in this order:

```text
1. What is an Array?
        ↓
2. Indexing & Memory
        ↓
3. Declaration & Initialization
        ↓
4. Input / Output
        ↓
5. Traversal
        ↓
6. Min / Max
        ↓
7. Sum / Product
        ↓
8. Linear Search
        ↓
9. Reverse
        ↓
10. Frequency / Duplicates
        ↓
11. Sorted Array
        ↓
12. Binary Search
        ↓
13. Two Pointers
        ↓
14. Rotation
        ↓
15. Prefix Sum
        ↓
16. Sliding Window
        ↓
17. Kadane's Algorithm
        ↓
18. 2D Arrays
        ↓
19. Array Interview Problems
        ↓
20. LeetCode / Coding Problems
```

> **Goal:** Do not memorize solutions. Learn to identify the pattern behind the problem. Once you can recognize whether a problem requires traversal, two pointers, hashing, prefix sum, sliding window, or binary search, solving array problems becomes much easier.
