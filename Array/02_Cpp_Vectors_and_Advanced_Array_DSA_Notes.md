# C++ Vectors & Advanced Array Patterns — DSA Notes

> These notes continue the Array chapter and cover **`vector`, vector functions, size vs capacity, dynamic growth, Kadane's Algorithm, Pair Sum, Two Pointers, Hashing, Majority Element, and Moore's Voting Algorithm** with detailed explanations, dry runs, complexity, mistakes, and practice questions.

---

# 1. Vector in C++

## Definition

A **vector** is a dynamic sequence container provided by the C++ Standard Library.

Unlike a built-in array whose size is fixed after creation, a vector can automatically grow or shrink as elements are added or removed.

```cpp
#include <vector>
using namespace std;

vector<int> nums;
```

A vector:

- stores elements of the same type
- supports index-based access
- manages its own memory
- can dynamically change its size
- provides many built-in functions
- is implemented as a class template

---

# 2. Why Do We Need Vectors?

Consider a built-in array:

```cpp
int arr[5];
```

Its capacity is fixed at 5 elements.

You cannot simply do:

```cpp
arr.push_back(10);
```

because a built-in array does not have `push_back()`.

A vector solves this:

```cpp
vector<int> arr;

arr.push_back(10);
arr.push_back(20);
arr.push_back(30);
```

Now:

```text
10 20 30
```

The vector automatically manages the storage required for its elements.

---

# 3. Vector Header File

To use vectors:

```cpp
#include <vector>
```

Example:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {

    vector<int> nums;

    nums.push_back(10);
    nums.push_back(20);

    cout << nums[0];

    return 0;
}
```

Output:

```text
10
```

---

# 4. Vector is a Template

Vectors are implemented as a class template.

Syntax:

```cpp
vector<data_type> vector_name;
```

Examples:

```cpp
vector<int> nums;
vector<double> prices;
vector<char> letters;
vector<string> names;
```

The type inside `< >` determines the type of elements stored.

---

# 5. Basic Vector Declaration

## Method 1 — Empty Vector

```cpp
vector<int> nums;
```

Initially:

```text
size = 0
```

---

## Method 2 — Empty Vector Using `{}`

```cpp
vector<int> nums = {};
```

This also creates an empty vector.

---

## Method 3 — Vector with a Given Size

```cpp
vector<int> nums(5);
```

This creates:

```text
[0][0][0][0][0]
```

The vector has:

```text
size = 5
```

### Important

This does **not** mean:

> "Reserve space for 5 elements and keep size 0."

It actually creates **5 elements** initialized to zero.

---

# 6. Vector with Size and Initial Value

```cpp
vector<int> nums(5, 10);
```

Result:

```text
[10][10][10][10][10]
```

So:

```text
vector<int>(size, value)
```

means:

> Create `size` elements, each initialized with `value`.

Example:

```cpp
vector<int> arr(4, -1);
```

Result:

```text
-1 -1 -1 -1
```

---

# 7. Vector Initialization Using Values

```cpp
vector<int> nums = {10, 20, 30, 40};
```

or:

```cpp
vector<int> nums{10, 20, 30, 40};
```

Result:

```text
Index:  0   1   2   3
Value: 10  20  30  40
```

---

# 8. Vector from Another Vector

```cpp
vector<int> a = {1, 2, 3};

vector<int> b(a);
```

Now:

```text
a = 1 2 3
b = 1 2 3
```

`b` is a separate vector containing copies of the elements.

---

# 9. Vector Size

Use:

```cpp
vec.size()
```

Example:

```cpp
vector<int> vec = {10, 20, 30};

cout << vec.size();
```

Output:

```text
3
```

### Definition

`size()` returns the **number of elements currently stored in the vector**.

---

# 10. Size vs Capacity

This is one of the most important vector concepts.

## Size

Number of actual elements currently stored.

## Capacity

Number of elements the vector can currently store in its allocated storage before requiring a reallocation.

Example:

```cpp
vector<int> v;

v.push_back(10);
```

Conceptually, you might have:

```text
size     = 1
capacity = some value >= 1
```

The exact capacity growth strategy is implementation-dependent.

---

# 11. `capacity()`

Use:

```cpp
vec.capacity()
```

Example:

```cpp
cout << vec.capacity();
```

It tells you how many elements can currently fit in the allocated storage without reallocating.

---

# 12. Size vs Capacity Example

Suppose:

```cpp
vector<int> v;

v.push_back(10);
v.push_back(20);
v.push_back(30);
```

You might observe:

```text
size = 3
capacity = 4
```

That means:

```text
Actual elements:
[10][20][30]

Allocated room:
[10][20][30][ ]
```

The exact capacity value is not guaranteed to be 4.

---

# 13. Important Correction About Capacity Doubling

A common beginner statement is:

> "Vector capacity always doubles when size becomes greater than capacity."

This is **not a C++ language guarantee**.

A vector grows its capacity when necessary, but the exact growth strategy is implementation-dependent.

You may observe doubling on some implementations:

```text
1 → 2 → 4 → 8 → 16
```

but you should not write DSA logic that depends on a guaranteed doubling factor.

The important concept is:

> **When the current capacity is insufficient, the vector reallocates storage with a larger capacity.**

---

# 14. `push_back()`

## Definition

`push_back()` adds an element to the end of the vector.

Example:

```cpp
vector<int> v;

v.push_back(10);
v.push_back(20);
v.push_back(30);
```

Result:

```text
10 20 30
```

---

# 15. `push_back()` Dry Run

Start:

```text
v = []
```

After:

```cpp
v.push_back(10);
```

```text
v = [10]
```

After:

```cpp
v.push_back(20);
```

```text
v = [10, 20]
```

After:

```cpp
v.push_back(30);
```

```text
v = [10, 20, 30]
```

---

# 16. Complexity of `push_back()`

Usually:

```text
Amortized time = O(1)
```

But an individual `push_back()` can take:

```text
O(n)
```

when reallocation is required and existing elements must be moved/copied.

### Important DSA concept

Do not say:

> `push_back()` is always O(1).

The more accurate statement is:

> **`push_back()` has amortized O(1) complexity, while an individual operation can be O(n) during reallocation.**

---

# 17. `pop_back()`

## Definition

`pop_back()` removes the last element.

Example:

```cpp
vector<int> v = {10, 20, 30};

v.pop_back();
```

Result:

```text
10 20
```

The removed value is:

```text
30
```

---

# 18. `pop_back()` Does Not Return the Removed Value

This is important.

Do not write:

```cpp
int x = v.pop_back();
```

because `pop_back()` returns `void`.

If you need the last value first:

```cpp
int x = v.back();

v.pop_back();
```

---

# 19. `front()`

`front()` returns a reference to the first element.

```cpp
vector<int> v = {10, 20, 30};

cout << v.front();
```

Output:

```text
10
```

---

# 20. `back()`

`back()` returns a reference to the last element.

```cpp
cout << v.back();
```

Output:

```text
30
```

---

# 21. Important Safety Rule for `front()` and `back()`

Do not call:

```cpp
v.front();
v.back();
```

on an empty vector.

Example:

```cpp
vector<int> v;

cout << v.front(); // invalid
```

Always understand whether the vector can be empty.

---

# 22. Accessing Elements with `[]`

You can access vector elements using the same index syntax as arrays.

```cpp
vector<int> v = {10, 20, 30};

cout << v[1];
```

Output:

```text
20
```

Complexity:

```text
O(1)
```

---

# 23. `at()`

`at()` accesses an element using an index.

```cpp
cout << v.at(1);
```

For a valid index:

```text
0 <= index < size
```

the element is returned.

Unlike `operator[]`, `at()` performs bounds checking and throws `std::out_of_range` when the index is invalid.

Example:

```cpp
vector<int> v = {10, 20, 30};

cout << v.at(5);
```

This throws an exception.

---

# 24. `[]` vs `at()`

| Feature | `v[index]` | `v.at(index)` |
|---|---|---|
| Access | Yes | Yes |
| Bounds checking | No | Yes |
| Invalid index | Undefined behavior | Throws `std::out_of_range` |
| Typical overhead | Lower | Bounds check |
| Complexity | O(1) | O(1) |

### DSA habit

Use `[]` when you know the index is valid and performance/simple syntax matters.

Use `at()` when explicit bounds checking is useful.

---

# 25. `clear()`

`clear()` removes all elements.

```cpp
vector<int> v = {10, 20, 30};

v.clear();
```

Now:

```text
size = 0
```

### Important

`clear()` destroys/removes the elements but does not necessarily reduce the vector's capacity.

So:

```text
size → 0
capacity → may remain unchanged
```

---

# 26. `empty()`

Use:

```cpp
v.empty()
```

It returns:

```text
true
```

if the vector contains no elements.

Example:

```cpp
if (v.empty()) {
    cout << "Vector is empty";
}
```

This is usually clearer than:

```cpp
if (v.size() == 0)
```

although both can express the same condition.

---

# 27. `insert()`

`insert()` inserts elements at a specified position.

Example:

```cpp
vector<int> v = {10, 20, 30};

v.insert(v.begin() + 1, 15);
```

Result:

```text
10 15 20 30
```

Why?

```text
v.begin()     → iterator to index 0
v.begin() + 1 → iterator to index 1
```

The new element is inserted before the element at index 1.

---

# 28. Inserting Multiple Copies

```cpp
vector<int> v = {10, 20, 30};

v.insert(v.begin() + 1, 3, 99);
```

Result:

```text
10 99 99 99 20 30
```

Syntax:

```cpp
insert(position, count, value)
```

---

# 29. `erase()`

Although not in the original function list, `erase()` is essential for vector DSA.

Remove one element:

```cpp
vector<int> v = {10, 20, 30};

v.erase(v.begin() + 1);
```

Result:

```text
10 30
```

The element at index 1 was removed.

---

# 30. Erasing a Range

```cpp
v.erase(v.begin() + 1, v.begin() + 3);
```

The range is:

```text
[first, last)
```

The first iterator is included, but the last iterator is excluded.

Example:

```text
10 20 30 40 50
```

Erase:

```cpp
v.erase(v.begin() + 1, v.begin() + 4);
```

Removes:

```text
20 30 40
```

Result:

```text
10 50
```

---

# 31. `resize()`

`resize()` changes the vector's size.

Example:

```cpp
vector<int> v = {1, 2, 3};

v.resize(5);
```

Result:

```text
1 2 3 0 0
```

For `int`, newly created elements are value-initialized to zero.

---

# 32. Resize to a Smaller Size

```cpp
vector<int> v = {1, 2, 3, 4, 5};

v.resize(3);
```

Result:

```text
1 2 3
```

The last two elements are removed.

---

# 33. `reserve()`

`reserve()` changes the **capacity**, not the size.

Example:

```cpp
vector<int> v;

v.reserve(100);
```

After this:

```text
size = 0
capacity >= 100
```

There are still **zero elements**.

This is a very important distinction:

```cpp
reserve(100);
```

does not create 100 elements.

---

# 34. `reserve()` vs `resize()`

| `reserve()` | `resize()` |
|---|---|
| Changes capacity | Changes size |
| Does not create elements | Creates/removes elements |
| `size` remains unchanged | `size` changes |
| Useful before many `push_back()` calls | Useful when you actually need a specific number of elements |

Example:

```cpp
vector<int> a;
a.reserve(5);
```

```text
size = 0
capacity >= 5
```

But:

```cpp
vector<int> b(5);
```

```text
size = 5
```

---

# 35. Range-Based For Loop

A vector can be traversed using:

```cpp
for (int x : vec) {
    cout << x << " ";
}
```

Example:

```cpp
vector<int> vec = {10, 20, 30};

for (int x : vec) {
    cout << x << " ";
}
```

Output:

```text
10 20 30
```

---

# 36. Modify Elements Using Reference

This:

```cpp
for (int x : vec) {
    x *= 2;
}
```

does not modify the vector because `x` is a copy.

Use:

```cpp
for (int &x : vec) {
    x *= 2;
}
```

Now the vector changes.

Example:

```text
Before:
1 2 3

After:
2 4 6
```

---

# 37. `auto` with Vector

You can write:

```cpp
for (auto x : vec) {
    cout << x << " ";
}
```

Or for modification:

```cpp
for (auto &x : vec) {
    x *= 2;
}
```

For read-only access without copying:

```cpp
for (const auto &x : vec) {
    cout << x << " ";
}
```

---

# 38. Vector Iterators

Vectors support iterators.

```cpp
vector<int> v = {10, 20, 30};

auto it = v.begin();

cout << *it;
```

Output:

```text
10
```

`begin()` points to the first element.

`end()` points **one position past the last element**.

Important:

```text
begin() → first element
end()   → one-past-last position
```

Do not dereference `end()`.

---

# 39. `begin()` and `end()`

Example:

```cpp
for (auto it = v.begin(); it != v.end(); ++it) {
    cout << *it << " ";
}
```

Output:

```text
10 20 30
```

This is the basis for many STL algorithms.

---

# 40. Vector and `sort()`

Include:

```cpp
#include <algorithm>
```

Then:

```cpp
sort(v.begin(), v.end());
```

Example:

```cpp
vector<int> v = {5, 2, 9, 1, 4};

sort(v.begin(), v.end());
```

Result:

```text
1 2 4 5 9
```

Typical complexity:

```text
O(n log n)
```

---

# 41. Descending Sort

```cpp
sort(v.begin(), v.end(), greater<int>());
```

Result:

```text
9 5 4 2 1
```

---

# 42. Vector vs Array

| Feature | Built-in Array | Vector |
|---|---|---|
| Size | Fixed | Dynamic |
| `push_back()` | ❌ | ✅ |
| `pop_back()` | ❌ | ✅ |
| `size()` member | ❌ | ✅ |
| `capacity()` | ❌ | ✅ |
| `front()` | ❌ | ✅ |
| `back()` | ❌ | ✅ |
| `at()` | ❌ | ✅ |
| Automatic growth | ❌ | ✅ |
| STL integration | Limited | Excellent |

---

# 43. Static vs Dynamic Allocation — Important Correction

A common beginner statement is:

> "Static is compile time and allocation is runtime."

This is too simplified.

There are several different concepts:

- compile time vs runtime
- storage duration
- stack vs heap
- fixed-size arrays vs dynamic containers

For DSA, remember the practical distinction:

```text
Built-in array with fixed size
    ↓
size cannot dynamically grow

vector
    ↓
can dynamically manage its storage
```

A vector itself is an object with automatic/dynamic storage depending on how it is created, while its element storage is managed dynamically by the vector.

---

# 44. XOR Properties

The uploaded material introduces XOR.

XOR operator:

```cpp
^
```

Important properties:

```text
x ^ x = 0
x ^ 0 = x
```

Also:

```text
x ^ y ^ x = y
```

because:

```text
x ^ x = 0
0 ^ y = y
```

XOR is extremely useful in array problems.

---

# 45. Example — Find Single Element

Suppose every number occurs twice except one:

```text
2 4 1 4 2
```

Answer:

```text
1
```

Using XOR:

```cpp
int ans = 0;

for (int x : nums) {
    ans ^= x;
}
```

Why?

```text
2 ^ 4 ^ 1 ^ 4 ^ 2

(2 ^ 2) ^ (4 ^ 4) ^ 1

0 ^ 0 ^ 1

= 1
```

Complexity:

```text
Time  = O(n)
Space = O(1)
```

### Important condition

This simple XOR technique requires the intended frequency property, typically:

> Every element appears exactly twice except one element that appears once.

---

# 46. Kadane's Algorithm

## Problem

Find the **maximum sum of a contiguous subarray**.

Example:

```text
arr = [-2, 3, -1, 5, -6]
```

Possible subarrays include:

```text
[-2]
[3]
[3,-1]
[3,-1,5]
[-1,5]
...
```

The maximum sum is:

```text
3 + (-1) + 5 = 7
```

---

# 47. Brute-Force Maximum Subarray Sum

The uploaded code uses nested loops.

Correct form:

```cpp
vector<int> arr = {2, 33, 4, 63, 12};

int n = arr.size();
int maxSum = INT_MIN;

for (int st = 0; st < n; st++) {

    int currSum = 0;

    for (int en = st; en < n; en++) {

        currSum += arr[en];

        maxSum = max(maxSum, currSum);
    }
}

cout << maxSum << endl;
```

---

# 48. Why Does the Brute-Force Code Work?

For every starting position:

```cpp
st
```

we extend the ending position:

```cpp
en
```

Example:

```text
1 2 3
```

For:

```text
st = 0
```

we calculate:

```text
1
1+2
1+2+3
```

For:

```text
st = 1
```

we calculate:

```text
2
2+3
```

For:

```text
st = 2
```

we calculate:

```text
3
```

Thus every contiguous subarray is considered.

---

# 49. Brute-Force Complexity

Number of start/end combinations is approximately:

```text
n²
```

Therefore:

```text
Time = O(n²)
Space = O(1)
```

This is much better than calculating every subarray sum from scratch with a third loop, which can become O(n³).

---

# 50. Kadane's Core Idea

Kadane's Algorithm improves the maximum-subarray problem to:

```text
O(n)
```

The key question at every element is:

> Should I extend the current subarray, or start a new subarray here?

For each element:

```text
current = max(current + arr[i], arr[i])
```

Meaning:

```text
Either:
1. Continue previous subarray
or
2. Start fresh from arr[i]
```

---

# 51. Kadane's Algorithm

```cpp
long long current = arr[0];
long long best = arr[0];

for (int i = 1; i < n; i++) {

    current = max(1LL * arr[i], current + arr[i]);

    best = max(best, current);
}

cout << best;
```

---

# 52. Kadane Dry Run

Consider:

```text
arr = [-2, 3, -1, 5, -6]
```

Start:

```text
current = -2
best = -2
```

At `3`:

```text
max(3, -2 + 3)
= max(3, 1)
= 3
```

So:

```text
current = 3
best = 3
```

At `-1`:

```text
max(-1, 3 + -1)
= max(-1, 2)
= 2
```

At `5`:

```text
max(5, 2 + 5)
= 7
```

At `-6`:

```text
max(-6, 7 - 6)
= 1
```

Final:

```text
best = 7
```

---

# 53. The Real Meaning of Kadane

A useful mental model:

```text
current = best sum ending at current index
best    = best sum found anywhere so far
```

This is more precise than simply saying:

> "Remove negative numbers."

Kadane's Algorithm does **not** simply remove every negative number.

For example:

```text
[4, -1, 5]
```

The `-1` is negative, but keeping it gives:

```text
4 + (-1) + 5 = 8
```

which is better than:

```text
4
```

So the correct logic is:

> Keep the previous subarray if extending it improves the sum; otherwise start a new subarray.

---

# 54. Important Kadane Edge Case

Consider:

```text
[-5, -2, -8]
```

The maximum subarray sum is:

```text
-2
```

If you incorrectly initialize:

```cpp
int current = 0;
int best = 0;
```

you may return:

```text
0
```

which is wrong if the problem requires a **non-empty** subarray.

Therefore a robust non-empty-subarray implementation starts from:

```cpp
arr[0]
```

---

# 55. Kadane Complexity

```text
Time  = O(n)
Space = O(1)
```

Comparison:

```text
Brute force → O(n²)
Kadane       → O(n)
```

This is a major optimization.

---

# 56. Pair Sum Problem

## Problem

Given an array and target, find two elements whose sum equals the target.

Example:

```text
nums = [2, 3, 5, 7]
target = 8
```

Possible answer:

```text
3 + 5 = 8
```

---

# 57. Brute-Force Pair Sum

```cpp
vector<int> pairSum(vector<int> nums, int target) {

    vector<int> ans;

    int n = nums.size();

    for (int i = 0; i < n; i++) {

        for (int j = i + 1; j < n; j++) {

            if (nums[i] + nums[j] == target) {

                ans.push_back(i);
                ans.push_back(j);

                return ans;
            }
        }
    }

    return ans;
}
```

---

# 58. Why `j = i + 1`?

We don't want:

```text
i == j
```

because that would use the same element twice.

We also don't need to check both:

```text
(i,j)
(j,i)
```

because they represent the same pair.

Therefore:

```cpp
for (int j = i + 1; j < n; j++)
```

avoids duplicate pair checks.

---

# 59. Pair Sum Complexity

Two nested loops:

```text
O(n²)
```

Extra result storage:

```text
O(1)
```

if the output is limited to two indices.

### Important nuance

If you pass:

```cpp
vector<int> nums
```

by value, the function may copy the vector.

For large inputs, prefer:

```cpp
vector<int> pairSum(const vector<int>& nums, int target)
```

This avoids copying the input vector.

---

# 60. Pair Sum on a Sorted Array — Two Pointers

If the array is sorted:

```text
2 3 4 5 7 9
```

we can use:

```text
left = 0
right = n - 1
```

Example:

```text
target = 9
```

---

# 61. Two-Pointer Logic

Calculate:

```cpp
sum = nums[left] + nums[right];
```

Then:

### If:

```text
sum == target
```

Pair found.

### If:

```text
sum > target
```

Decrease `right`.

Why?

Because the array is sorted, moving right leftward reduces the value.

### If:

```text
sum < target
```

Increase `left`.

Why?

Because moving left rightward increases the value.

---

# 62. Two-Pointer Example

Array:

```text
2 3 4 5 7 9
```

Target:

```text
9
```

Start:

```text
left = 0 → 2
right = 5 → 9
```

Sum:

```text
2 + 9 = 11
```

Too large:

```text
right--
```

Now:

```text
2 + 7 = 9
```

Found.

Indices:

```text
0 and 4
```

---

# 63. Two-Pointer Code

```cpp
vector<int> pairSum(const vector<int>& nums, int target) {

    vector<int> ans;

    int left = 0;
    int right = nums.size() - 1;

    while (left < right) {

        int sum = nums[left] + nums[right];

        if (sum == target) {

            ans.push_back(left);
            ans.push_back(right);

            return ans;
        }

        else if (sum > target) {
            right--;
        }

        else {
            left++;
        }
    }

    return ans;
}
```

---

# 64. Critical Condition for Two-Pointer Pair Sum

The simple:

```text
if sum > target → right--
if sum < target → left++
```

logic depends on the array being **sorted in ascending order**.

For:

```text
2 3 4 5 7 9
```

it works.

For:

```text
2 7 3 9 4 5
```

it does not work reliably.

---

# 65. Pair Sum Complexity — Two Pointers

```text
Time  = O(n)
Space = O(1)
```

assuming the input is already sorted and no additional storage is required.

### But what if the array is unsorted?

You have options.

---

# 66. Pair Sum on an Unsorted Array

A common optimal-average approach uses hashing.

For each value:

```text
needed = target - current
```

Check whether `needed` has already been seen.

Example:

```text
nums = [2, 7, 11, 15]
target = 9
```

Start:

```text
current = 2
needed = 9 - 2 = 7
```

Store `2`.

Next:

```text
current = 7
needed = 2
```

`2` is already present.

Pair found.

---

# 67. Hashing Pair Sum

Typical code:

```cpp
vector<int> twoSum(const vector<int>& nums, int target) {

    unordered_map<int, int> seen;

    for (int i = 0; i < nums.size(); i++) {

        int needed = target - nums[i];

        if (seen.count(needed)) {
            return {seen[needed], i};
        }

        seen[nums[i]] = i;
    }

    return {};
}
```

Typical complexity:

```text
Average Time = O(n)
Space        = O(n)
```

Worst-case hash-table complexity can degrade, so the O(n) claim is generally an average/expected complexity statement.

---

# 68. Three Pair-Sum Approaches

| Approach | Array requirement | Time | Extra Space |
|---|---|---:|---:|
| Brute force | Any | O(n²) | O(1) |
| Two pointers | Sorted | O(n) | O(1) |
| Hashing | Any | O(n) average | O(n) |

This is an important interview comparison.

---

# 69. Majority Element

## Definition

An element is a **majority element** if it appears more than:

```text
n / 2
```

times in an array of size `n`.

Example:

```text
[2, 2, 1, 2, 3, 2, 2]
```

Here:

```text
n = 7
```

Majority threshold:

```text
7 / 2 = 3
```

The value `2` occurs 5 times.

Since:

```text
5 > 3
```

`2` is the majority element.

---

# 70. Important Difference: More Than vs At Least

Majority means:

```text
frequency > n/2
```

not:

```text
frequency >= n/2
```

For:

```text
n = 6
```

a majority must occur at least:

```text
4
```

times.

Three occurrences is not a majority because:

```text
3 > 3
```

is false.

---

# 71. Brute-Force Majority Element

The original approach checks the frequency of every value.

```cpp
int majorityElement(vector<int> nums) {

    int n = nums.size();

    for (int val : nums) {

        int freq = 0;

        for (int el : nums) {

            if (el == val) {
                freq++;
            }
        }

        if (freq > n / 2) {
            return val;
        }
    }

    return -1;
}
```

Complexity:

```text
Time  = O(n²)
Space = O(1)
```

---

# 72. Sorting-Based Majority Element

Sort the array:

```cpp
sort(nums.begin(), nums.end());
```

If a majority element exists, it must occupy the middle position.

Therefore:

```cpp
int candidate = nums[n / 2];
```

For the classic majority-element problem where existence is guaranteed, this candidate is the majority element.

### Example

```text
Input:
2 1 2 2 3 2 2

Sorted:
1 2 2 2 2 2 3
```

Middle:

```text
index = 7 / 2 = 3
```

Value:

```text
2
```

---

# 73. Sorting Approach Complexity

Sorting:

```text
O(n log n)
```

Then checking/returning the candidate:

```text
O(1)
```

Overall:

```text
O(n log n)
```

If the array is sorted in place:

```text
Extra space depends on the sorting implementation/standard-library guarantees and recursion details.
```

For the common DSA comparison, the key point is that sorting is slower than Moore's Voting Algorithm in time.

---

# 74. Moore's Voting Algorithm

## Definition

**Moore's Voting Algorithm**, commonly called the **Boyer-Moore Majority Vote Algorithm**, finds a majority element in:

```text
O(n) time
O(1) extra space
```

when a majority element exists.

The algorithm maintains:

```text
candidate
count
```

---

# 75. Core Idea of Moore's Voting

Think of the majority element as having enough votes to survive cancellation.

Whenever we see:

```text
same as candidate
```

increase count.

Whenever we see:

```text
different from candidate
```

decrease count.

If count becomes zero:

```text
choose a new candidate
```

The majority element cannot be completely canceled because it occurs more than all other elements combined.

---

# 76. Moore's Voting Code

```cpp
int majorityElement(const vector<int>& nums) {

    int candidate = 0;
    int count = 0;

    for (int value : nums) {

        if (count == 0) {
            candidate = value;
        }

        if (value == candidate) {
            count++;
        }
        else {
            count--;
        }
    }

    return candidate;
}
```

This is sufficient if the problem **guarantees that a majority element exists**.

---

# 77. Moore's Voting Dry Run

Consider:

```text
2 2 1 1 1 2 2
```

Start:

```text
candidate = ?
count = 0
```

### Value = 2

Count is zero:

```text
candidate = 2
```

Same:

```text
count = 1
```

### Value = 2

Same:

```text
count = 2
```

### Value = 1

Different:

```text
count = 1
```

### Value = 1

Different:

```text
count = 0
```

### Value = 1

Count is zero:

```text
candidate = 1
count = 1
```

### Value = 2

Different:

```text
count = 0
```

### Value = 2

Count is zero:

```text
candidate = 2
count = 1
```

Final candidate:

```text
2
```

---

# 78. Why Does Moore's Voting Work?

Suppose a majority element appears:

```text
> n/2
```

times.

Therefore, its frequency is greater than the total frequency of all non-majority elements combined.

Pairing:

```text
majority element
+
different element
```

cancels one majority vote against one non-majority vote.

Because there are more majority votes, some majority votes remain uncanceled.

Therefore the final candidate must be the majority element.

---

# 79. Candidate vs Verified Majority

This is a critical point.

Moore's algorithm's first pass gives a **candidate**.

If the problem does **not guarantee** that a majority element exists, you should verify it.

Example:

```text
[1, 2, 3]
```

Moore's process may return a candidate, but there is no majority element because:

```text
frequency of each = 1
n/2 = 1
```

and:

```text
1 > 1
```

is false.

---

# 80. Moore's Voting with Verification

```cpp
int majorityElement(const vector<int>& nums) {

    int candidate = 0;
    int count = 0;

    // Phase 1: find candidate
    for (int value : nums) {

        if (count == 0) {
            candidate = value;
        }

        if (value == candidate) {
            count++;
        }
        else {
            count--;
        }
    }

    // Phase 2: verify candidate
    int freq = 0;

    for (int value : nums) {

        if (value == candidate) {
            freq++;
        }
    }

    if (freq > nums.size() / 2) {
        return candidate;
    }

    return -1;
}
```

Complexity:

```text
Time  = O(n)
Space = O(1)
```

---

# 81. Majority Element Approaches

| Approach | Time | Extra Space | Main Idea |
|---|---:|---:|---|
| Brute force | O(n²) | O(1) | Count every value |
| Hashing | O(n) average | O(n) | Store frequencies |
| Sorting | O(n log n) | Depends | Middle element |
| Moore's Voting | O(n) | O(1) | Cancel opposing votes |

---

# 82. Vector Passing: Value vs Reference

The original pair-sum code uses:

```cpp
vector<int> pairSum(vector<int> nums, int target)
```

This passes the vector by value, which creates a copy.

For read-only input, prefer:

```cpp
vector<int> pairSum(const vector<int>& nums, int target)
```

Meaning:

```text
const
 ↓
function cannot modify nums

&
 ↓
avoid copying the entire vector
```

This is a very important C++ DSA habit.

---

# 83. `vector<int> nums` vs `const vector<int>& nums`

### By value

```cpp
void solve(vector<int> nums)
```

Conceptually:

```text
original vector
      ↓
    COPY
      ↓
function
```

Potential extra:

```text
O(n)
```

copy cost.

### By const reference

```cpp
void solve(const vector<int>& nums)
```

Conceptually:

```text
original vector
      ↓
function accesses it
      ↓
no copy
```

Usually preferred when the function only needs to read the vector.

---

# 84. If Function Needs to Modify the Vector

Use:

```cpp
void modify(vector<int>& nums) {
    nums[0] = 100;
}
```

The `&` allows the function to modify the original vector.

If you don't want modification:

```cpp
void print(const vector<int>& nums)
```

---

# 85. Important Code Corrections from the Source

Several snippets in the original notes are conceptually correct but contain syntax or implementation issues.

## Issue 1 — `ans` not declared

This:

```cpp
ans.push_back(i);
```

requires:

```cpp
vector<int> ans;
```

inside the function.

Correct:

```cpp
vector<int> pairSum(const vector<int>& nums, int target) {

    vector<int> ans;

    ...
}
```

---

## Issue 2 — Missing `&` in output

Incorrect:

```cpp
cout << ans[0] << " "< ans[1];
```

Correct:

```cpp
cout << ans[0] << " " << ans[1];
```

---

## Issue 3 — Missing `vector<int>` return syntax details

Correct function:

```cpp
vector<int> pairSum(const vector<int>& nums, int target)
```

---

## Issue 4 — Sorting requires `<algorithm>`

If you use:

```cpp
sort(nums.begin(), nums.end());
```

include:

```cpp
#include <algorithm>
```

---

## Issue 5 — Majority-element sorting code

A safer/simple approach is:

```cpp
sort(nums.begin(), nums.end());

return nums[nums.size() / 2];
```

when the problem guarantees a majority exists.

If existence is not guaranteed, verify the candidate.

---

# 86. Common Vector Mistakes

## Mistake 1 — Confusing size and capacity

```cpp
vector<int> v;

v.reserve(10);
```

does not mean:

```text
10 elements exist
```

It means approximately:

```text
space for at least 10 elements has been reserved
```

---

## Mistake 2 — Assuming capacity always doubles

Do not rely on:

```text
capacity *= 2
```

as a C++ guarantee.

---

## Mistake 3 — Calling `front()` on empty vector

```cpp
vector<int> v;

cout << v.front();
```

Invalid.

---

## Mistake 4 — Calling `back()` after `pop_back()` without checking

```cpp
v.pop_back();
cout << v.back();
```

If the vector was originally size 1, it is now empty.

---

## Mistake 5 — Using invalid index

```cpp
v[100]
```

is invalid if the vector has fewer than 101 elements.

---

## Mistake 6 — Assuming `at()` silently returns something

It does not.

An invalid index causes an exception.

---

# 87. Important Vector Complexity Table

| Operation | Typical Complexity |
|---|---:|
| Access `v[i]` | O(1) |
| `front()` | O(1) |
| `back()` | O(1) |
| `push_back()` | Amortized O(1) |
| `pop_back()` | O(1) |
| `insert()` at end | Amortized O(1) when equivalent to append |
| `insert()` in middle | O(n) |
| `erase()` in middle | O(n) |
| `clear()` | O(n) |
| `size()` | O(1) |
| `empty()` | O(1) |
| `reserve()` | May reallocate; complexity depends on reallocation |
| `resize()` | Depends on operation; can be O(n) |

---

# 88. Vector Memory Model

Conceptually:

```text
Vector object
     │
     ├── pointer ───────────────┐
     ├── size                   │
     └── capacity               │
                                ↓
                         Dynamic storage
                    ┌────┬────┬────┬────┐
                    │ 10 │ 20 │ 30 │    │
                    └────┴────┴────┴────┘
```

The exact internal representation is implementation-specific, but this is a useful conceptual model.

---

# 89. Reallocation

Suppose:

```text
size = capacity
```

and you execute:

```cpp
push_back(x);
```

The current storage may not have enough room.

The vector can:

```text
1. allocate larger storage
2. move/copy existing elements
3. add the new element
4. release old storage
```

Conceptually:

```text
Old:
[10][20][30]

        ↓ reallocation

New:
[10][20][30][40][ ][ ]
```

This is why one individual `push_back()` can cost O(n).

---

# 90. Why Amortized O(1)?

Although some insertions require expensive reallocation, they do not happen every time.

Across many `push_back()` operations, the total cost averages out.

Therefore:

```text
push_back()
     ↓
amortized O(1)
```

This concept is called **amortized analysis**.

---

# 91. Pair Sum Pattern Recognition

When you see:

> "Find two numbers whose sum equals target"

Ask:

### Is the array sorted?

If yes:

```text
Two pointers
```

### Is it unsorted?

Consider:

```text
Hashing
```

### Are constraints tiny?

Brute force may be acceptable:

```text
O(n²)
```

### Do you need original indices?

Be careful if sorting because sorting changes positions.

---

# 92. Kadane Pattern Recognition

When you see:

> "Maximum sum of a contiguous subarray"

Think:

```text
Kadane's Algorithm
```

Keywords:

```text
maximum subarray
largest contiguous sum
maximum sum contiguous segment
```

---

# 93. XOR Pattern Recognition

When you see:

> Every number appears twice except one.

Think:

```text
XOR
```

Because:

```text
x ^ x = 0
x ^ 0 = x
```

---

# 94. Majority Element Pattern Recognition

When you see:

> Element appears more than n/2 times.

Think:

```text
Moore's Voting Algorithm
```

If no majority is guaranteed:

```text
candidate + verification
```

---

# 95. Questions You Must Be Able to Answer

## Vector Basics

1. What is a vector?
2. Why is vector called a dynamic array?
3. How is vector different from a built-in array?
4. What does `vector<int> v(5)` create?
5. What does `vector<int> v(5, 10)` create?
6. What is the difference between `size()` and `capacity()`?
7. What does `push_back()` do?
8. What does `pop_back()` do?
9. Does `pop_back()` return the removed value?
10. What does `front()` return?
11. What does `back()` return?
12. What happens when `at()` receives an invalid index?
13. What does `clear()` do?
14. Does `clear()` necessarily reduce capacity?
15. What does `empty()` do?
16. What does `reserve()` do?
17. Difference between `reserve()` and `resize()`?
18. What is reallocation?
19. Why can `push_back()` sometimes be O(n)?
20. Why is `push_back()` amortized O(1)?

---

# 96. Algorithm Questions

21. What is Kadane's Algorithm?
22. What problem does Kadane solve?
23. Why is brute-force maximum subarray O(n²)?
24. What does `current` represent in Kadane?
25. What does `best` represent?
26. Why should Kadane handle all-negative arrays carefully?
27. What is Pair Sum?
28. What is the brute-force complexity?
29. Why does two-pointer Pair Sum require sorting?
30. Why do we move `right` when sum is too large?
31. Why do we move `left` when sum is too small?
32. How can hashing solve Pair Sum in O(n) average time?
33. What is the space complexity of hashing Pair Sum?
34. What is a majority element?
35. Why is the threshold `> n/2`?
36. How does sorting help find majority?
37. What is Moore's Voting Algorithm?
38. Why does cancellation work?
39. What is the difference between a candidate and a verified majority?
40. When should Moore's result be verified?

---

# 97. Coding Questions — Easy

### Q1. Create an empty vector and add five numbers using `push_back()`.

### Q2. Print the vector using a normal `for` loop.

### Q3. Print the vector using a range-based loop.

### Q4. Print first and last elements.

### Q5. Remove the last element.

### Q6. Insert `100` at index `2`.

### Q7. Delete the element at index `3`.

### Q8. Find the minimum element.

### Q9. Find the maximum element.

### Q10. Find the sum of all elements.

---

# 98. Coding Questions — Intermediate

### Q11. Reverse a vector in-place.

### Q12. Find the first occurrence of a target.

### Q13. Find the last occurrence.

### Q14. Count target frequency.

### Q15. Move all zeros to the end.

### Q16. Find the second largest distinct element.

### Q17. Check whether a vector is sorted.

### Q18. Find duplicate elements.

### Q19. Find the unique element using XOR.

### Q20. Rotate a vector left by `k`.

---

# 99. Coding Questions — Advanced

### Q21. Maximum subarray sum using brute force.

### Q22. Maximum subarray sum using Kadane.

### Q23. Return the actual maximum-sum subarray.

### Q24. Two Sum using nested loops.

### Q25. Two Sum using hashing.

### Q26. Two Sum on sorted array using two pointers.

### Q27. Find majority element using brute force.

### Q28. Find majority element using sorting.

### Q29. Find majority element using Moore's Voting.

### Q30. Find majority element and verify whether it actually exists.

---

# 100. Final Mental Map

```text
VECTOR
│
├── Dynamic sequence
│
├── Creation
│   ├── vector<int> v;
│   ├── vector<int> v = {};
│   ├── vector<int> v(5);
│   ├── vector<int> v(5, 10);
│   └── vector<int> v = {1,2,3};
│
├── Access
│   ├── []
│   ├── at()
│   ├── front()
│   └── back()
│
├── Modification
│   ├── push_back()
│   ├── pop_back()
│   ├── insert()
│   ├── erase()
│   ├── clear()
│   └── resize()
│
├── Memory
│   ├── size()
│   ├── capacity()
│   ├── reserve()
│   └── reallocation
│
└── DSA Patterns
    ├── XOR
    ├── Kadane
    ├── Two Pointers
    ├── Hashing
    └── Moore's Voting
```

---

# 101. Final Complexity Cheat Sheet

```text
Vector access              → O(1)
Vector size                → O(1)
Vector front/back          → O(1)
push_back                  → amortized O(1)
pop_back                   → O(1)
middle insertion           → O(n)
middle deletion            → O(n)

Brute-force Pair Sum       → O(n²)
Hashing Pair Sum           → O(n) average, O(n) space
Sorted Two-Pointer PairSum → O(n), O(1) extra space

Brute-force Max Subarray   → O(n²)
Kadane                     → O(n), O(1)

Brute-force Majority       → O(n²)
Sorting Majority           → O(n log n)
Moore's Voting             → O(n), O(1)

XOR unique-element problem → O(n), O(1)
```

---

# 102. The Most Important Things to Remember

```text
1. Vector = dynamic sequence container.
2. size = actual number of elements.
3. capacity = allocated storage available for elements.
4. reserve() changes capacity, not size.
5. resize() changes size.
6. push_back() is amortized O(1), not guaranteed O(1) every time.
7. at() performs bounds checking.
8. [] does not perform bounds checking.
9. pop_back() removes the last element and returns nothing.
10. x ^ x = 0.
11. x ^ 0 = x.
12. Kadane = maximum contiguous subarray sum.
13. Two pointers Pair Sum requires sorted data.
14. Hashing Pair Sum works on unsorted data in O(n) average time.
15. Majority = frequency > n/2.
16. Moore's Voting = O(n) time and O(1) extra space.
17. Moore's candidate must be verified if majority existence is not guaranteed.
18. Pass large vectors using const reference when you only need to read them.
19. Always inspect constraints before choosing an algorithm.
20. Do not memorize code without understanding the pattern.
```

---

# 103. Recommended Study Sequence

Study these concepts in this exact order:

```text
Vector basics
    ↓
size vs capacity
    ↓
push_back / pop_back
    ↓
front / back / at
    ↓
insert / erase
    ↓
clear / empty
    ↓
resize / reserve
    ↓
iterators
    ↓
sorting
    ↓
XOR problems
    ↓
Brute-force subarray problems
    ↓
Kadane's Algorithm
    ↓
Pair Sum brute force
    ↓
Pair Sum hashing
    ↓
Pair Sum two pointers
    ↓
Majority brute force
    ↓
Majority sorting
    ↓
Moore's Voting
    ↓
Mixed array problems
```

> **DSA rule:** First understand the brute-force solution, then identify what repeated work is happening, and finally optimize it using the correct pattern. This is how you move from `O(n²)` to `O(n)` instead of merely memorizing an "optimal" code template.
