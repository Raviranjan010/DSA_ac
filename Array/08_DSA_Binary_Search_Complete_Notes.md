# 📘 DSA Notes: Binary Search

## Complete Guide — Iterative + Recursive Binary Search

---

# 1. What Is Binary Search?

**Binary Search** is a searching algorithm used to efficiently find a target element in a **sorted array**.

Instead of checking every element one by one, binary search repeatedly divides the search space into two halves.

### Core Idea

```text
Sorted Array
     ↓
Find middle element
     ↓
Compare target with middle
     ↓
Eliminate one half
     ↓
Repeat
```

Because half of the search space is eliminated at every step, binary search has:

```text
Time Complexity = O(log n)
```

---

# 2. Most Important Requirement

Binary search requires the data to be sorted according to the search condition.

For an ascending array:

```text
1  3  5  7  9  11
```

we can determine:

```text
target < mid
```

or:

```text
target > mid
```

and safely eliminate one half.

### Example

```text
1  3  5  7  9  11
         ↑
        mid
```

If:

```text
target = 3
mid = 7
```

Since:

```text
3 < 7
```

the target can only be in:

```text
left half
```

We can eliminate:

```text
7  9  11
```

---

# 3. Why Must the Array Be Sorted?

Suppose:

```text
arr = [7, 2, 9, 1, 5]
```

The middle element is:

```text
9
```

If:

```text
target = 5
```

we know:

```text
5 < 9
```

but we cannot conclude that `5` is on the left.

It could be anywhere.

Therefore, binary search cannot safely eliminate half of an unsorted array.

### ⭐ Rule

> **Binary Search → Sorted Data**

---

# 4. Ascending Order

For ascending order:

```text
1  2  3  4  5  6  7
```

The smallest element is on the left.

The largest element is on the right.

If:

```text
target > arr[mid]
```

the target must be to the right.

Therefore:

```cpp
st = mid + 1;
```

If:

```text
target < arr[mid]
```

the target must be to the left.

Therefore:

```cpp
end = mid - 1;
```

---

# 5. The Three Important Variables

Binary search commonly uses:

```cpp
int st = 0;
int end = n - 1;
```

and:

```cpp
int mid;
```

Meaning:

```text
st  → beginning of current search space
end → end of current search space
mid → middle of current search space
```

---

# 6. Initial Search Space

Suppose:

```text
arr = [1,2,3,4,5,6,7]
```

Indices:

```text
 0 1 2 3 4 5 6
```

Initially:

```text
st = 0
end = 6
```

Search space:

```text
[1 2 3 4 5 6 7]
 ↑           ↑
st          end
```

---

# 7. Finding the Middle

The basic formula is:

```cpp
int mid = (st + end) / 2;
```

This works logically, but there is a possible integer overflow issue.

Prefer:

```cpp
int mid = st + (end - st) / 2;
```

---

# 8. Why Is `(st + end) / 2` Potentially Dangerous?

Suppose:

```text
st = INT_MAX - 10
end = INT_MAX
```

Then:

```cpp
st + end
```

may exceed the maximum value representable by `int`.

This can cause integer overflow.

Instead:

```cpp
st + (end - st) / 2
```

calculates the same midpoint without directly adding two potentially huge indices.

### ⭐ Best Practice

Always prefer:

```cpp
int mid = st + (end - st) / 2;
```

---

# 9. Binary Search Conditions

For ascending order:

### Case 1 — Target is greater

```cpp
if(target > arr[mid]) {
    st = mid + 1;
}
```

Meaning:

```text
Target is on the right.
```

---

### Case 2 — Target is smaller

```cpp
else if(target < arr[mid]) {
    end = mid - 1;
}
```

Meaning:

```text
Target is on the left.
```

---

### Case 3 — Target found

```cpp
else {
    return mid;
}
```

Because:

```cpp
target == arr[mid]
```

---

# 10. Iterative Binary Search

## Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int binarySearch(const vector<int>& arr, int target) {

    int st = 0;
    int end = arr.size() - 1;

    while(st <= end) {

        int mid = st + (end - st) / 2;

        if(target > arr[mid]) {

            st = mid + 1;

        }
        else if(target < arr[mid]) {

            end = mid - 1;

        }
        else {

            return mid;
        }
    }

    return -1;
}
```

---

# 11. Why `st <= end`?

This condition is extremely important:

```cpp
while(st <= end)
```

The search is valid while the search range contains at least one element.

### Example

```text
st = 3
end = 3
```

There is still one element:

```text
index 3
```

So we must check it.

Therefore:

```text
st == end
```

must be allowed.

If we used:

```cpp
while(st < end)
```

we could skip the final candidate.

### ⭐ Rule

For the standard inclusive binary-search implementation:

```cpp
while(st <= end)
```

---

# 12. Why `mid + 1` and `mid - 1`?

Suppose:

```text
arr[mid] < target
```

We already know:

```text
arr[mid] != target
```

Therefore, we do not need to search `mid` again.

So:

```cpp
st = mid + 1;
```

Similarly:

```text
arr[mid] > target
```

means:

```text
mid cannot be the answer
```

Therefore:

```cpp
end = mid - 1;
```

---

# 13. Dry Run — Target Found

Array:

```text
arr = [1,2,3,4,5,6,7]
```

Target:

```text
5
```

Indices:

```text
0 1 2 3 4 5 6
1 2 3 4 5 6 7
```

---

## Iteration 1

```text
st = 0
end = 6
```

```text
mid = 0 + (6 - 0)/2
    = 3
```

```text
arr[mid] = 4
```

Target:

```text
5
```

Since:

```text
5 > 4
```

move right:

```text
st = mid + 1
   = 4
```

---

## Iteration 2

```text
st = 4
end = 6
```

```text
mid = 4 + (6 - 4)/2
    = 5
```

```text
arr[5] = 6
```

Since:

```text
5 < 6
```

move left:

```text
end = mid - 1
    = 4
```

---

## Iteration 3

```text
st = 4
end = 4
```

```text
mid = 4
```

```text
arr[4] = 5
```

Target found.

Return:

```text
4
```

---

# 14. Dry Run Table

For:

```text
arr = [1,2,3,4,5,6,7]
target = 5
```

| Iteration | `st` | `end` | `mid` | `arr[mid]` | Decision |
|---|---:|---:|---:|---:|---|
| 1 | 0 | 6 | 3 | 4 | Go right |
| 2 | 4 | 6 | 5 | 6 | Go left |
| 3 | 4 | 4 | 4 | 5 | Found |

Answer:

```text
4
```

---

# 15. Dry Run — Target Not Found

Array:

```text
[1,2,3,4,5,6,7]
```

Target:

```text
10
```

Iteration 1:

```text
mid = 3
arr[mid] = 4
```

Since:

```text
10 > 4
```

move:

```text
st = 4
```

Iteration 2:

```text
mid = 5
arr[mid] = 6
```

Since:

```text
10 > 6
```

move:

```text
st = 6
```

Iteration 3:

```text
mid = 6
arr[mid] = 7
```

Since:

```text
10 > 7
```

move:

```text
st = 7
```

Now:

```text
st = 7
end = 6
```

Therefore:

```text
st > end
```

Search is over.

Return:

```cpp
-1;
```

---

# 16. Why Return `-1`?

Array indices normally begin at:

```text
0
```

Therefore:

```text
-1
```

is not a valid index.

So it is commonly used to indicate:

```text
Target not found
```

---

# 17. Time Complexity

Binary search repeatedly cuts the search space approximately in half:

```text
n
n/2
n/4
n/8
n/16
...
```

After `k` steps:

```text
n / 2^k
```

When only one element remains:

```text
n / 2^k = 1
```

Therefore:

```text
n = 2^k
```

Taking logarithm base 2:

```text
log₂(n) = k
```

Therefore:

```text
Time Complexity = O(log n)
```

---

# 18. Why Is It `O(log n)`?

The important point is not that the loop performs a fixed number of operations.

The number of iterations depends on how many times we can divide `n` by `2`.

Example:

```text
n = 8

8 → 4 → 2 → 1
```

Approximately:

```text
3 divisions
```

and:

```text
log₂(8) = 3
```

For:

```text
n = 16
```

```text
16 → 8 → 4 → 2 → 1
```

```text
log₂(16) = 4
```

So the number of iterations grows very slowly.

---

# 19. Complexity Comparison

For large `n`:

```text
O(1)
O(log n)
O(n)
O(n log n)
O(n²)
O(2ⁿ)
O(n!)
```

Binary search:

```text
O(log n)
```

This is much faster than linear search:

```text
O(n)
```

for large sorted arrays.

---

# 20. Binary Search vs Linear Search

| Feature | Linear Search | Binary Search |
|---|---|---|
| Data requirement | No sorting required | Sorted data required |
| Approach | Check one by one | Eliminate half |
| Worst-case time | O(n) | O(log n) |
| Best case | O(1) | O(1) |
| Random access helpful? | Not required | Yes |
| Main idea | Sequential scan | Divide search space |

---

# 21. Important Trade-Off

Binary search is not automatically better than linear search.

If the data is unsorted:

```text
[7,2,9,1,5]
```

you cannot directly use standard binary search.

You could sort first:

```text
O(n log n)
```

and then binary search:

```text
O(log n)
```

For a single search, sorting may cost more than simply doing:

```text
O(n)
```

linear search.

But if you need many searches on the same data, sorting once can make binary search very useful.

---

# 22. Recursive Binary Search

Binary search can also be implemented using recursion.

The idea is exactly the same:

```text
Check middle
    ↓
Target greater?
    ↓
Search right half

Target smaller?
    ↓
Search left half

Target equal?
    ↓
Return index
```

---

# 23. Recursive Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int recursiveBinarySearch(
    const vector<int>& arr,
    int target,
    int st,
    int end
) {

    if(st > end) {
        return -1;
    }

    int mid = st + (end - st) / 2;

    if(target > arr[mid]) {

        return recursiveBinarySearch(
            arr,
            target,
            mid + 1,
            end
        );
    }

    else if(target < arr[mid]) {

        return recursiveBinarySearch(
            arr,
            target,
            st,
            mid - 1
        );
    }

    else {

        return mid;
    }
}
```

---

# 24. Recursive Base Case

This is the most important part:

```cpp
if(st > end) {
    return -1;
}
```

Why?

Because:

```text
st > end
```

means the search range is empty.

Example:

```text
st = 5
end = 4
```

There is no valid index to search.

Therefore:

```text
Target does not exist.
```

---

# 25. Recursive Dry Run

Array:

```text
[1,2,3,4,5,6,7]
```

Target:

```text
5
```

Initial:

```text
st = 0
end = 6
```

Middle:

```text
mid = 3
arr[3] = 4
```

Since:

```text
5 > 4
```

call:

```cpp
recursiveBinarySearch(arr, 5, 4, 6);
```

Now:

```text
st = 4
end = 6
```

Middle:

```text
mid = 5
arr[5] = 6
```

Since:

```text
5 < 6
```

call:

```cpp
recursiveBinarySearch(arr, 5, 4, 4);
```

Now:

```text
mid = 4
arr[4] = 5
```

Found.

Return:

```text
4
```

---

# 26. Recursive Call Stack

Conceptually:

```text
binarySearch(0,6)
       ↓
binarySearch(4,6)
       ↓
binarySearch(4,4)
       ↓
return 4
```

Then the result returns back through the recursive calls.

---

# 27. Iterative vs Recursive Binary Search

| Feature | Iterative | Recursive |
|---|---|---|
| Loop | `while` | Function calls |
| Time | O(log n) | O(log n) |
| Extra stack space | O(1) | O(log n) |
| Code | Usually simpler | Often elegant |
| Risk | No recursion depth | Uses call stack |
| Practical choice | Usually preferred | Good for learning/recursive patterns |

Important:

The **time complexity is O(log n)** for both.

But recursive binary search uses additional call-stack space:

```text
O(log n)
```

while the iterative version uses:

```text
O(1)
```

auxiliary space.

---

# 28. Correction to the Provided Code

Your original function declaration was:

```cpp
int binarySearch(vector<int>)
```

This is incomplete because the function needs:

```text
array
target
```

A correct version is:

```cpp
int binarySearch(const vector<int>& arr, int target)
```

---

# 29. Why Use `const vector<int>&`?

Instead of:

```cpp
vector<int> arr
```

we can use:

```cpp
const vector<int>& arr
```

This avoids copying the entire vector.

### By value

```cpp
vector<int> arr
```

creates a copy.

For an array of `n` elements, copying costs:

```text
O(n)
```

### By const reference

```cpp
const vector<int>& arr
```

does not copy the vector.

So it is more efficient.

---

# 30. Important Issue in Your Example

You wrote:

```cpp
vector<int> arr1 = {1,2,-2,44,3,7};
```

This array is **not sorted**.

Therefore standard binary search cannot be correctly applied to it.

Sort it first:

```cpp
vector<int> arr1 = {-2,1,2,3,7,44};
```

or:

```cpp
sort(arr1.begin(), arr1.end());
```

Then binary search can be used.

---

# 31. Another Unsorted Example

You wrote:

```cpp
vector<int> arr2 = {-1,2,4,66,32,76};
```

This is also not sorted.

Correct ascending order:

```text
-1 2 4 32 66 76
```

If you want binary search:

```cpp
sort(arr2.begin(), arr2.end());
```

---

# 32. Correct Complete Program

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int binarySearch(const vector<int>& arr, int target) {

    int st = 0;
    int end = arr.size() - 1;

    while(st <= end) {

        int mid = st + (end - st) / 2;

        if(target > arr[mid]) {

            st = mid + 1;
        }

        else if(target < arr[mid]) {

            end = mid - 1;
        }

        else {

            return mid;
        }
    }

    return -1;
}

int main() {

    vector<int> arr = {1, 2, 3, 4, 7, 44};

    int target = 7;

    cout << binarySearch(arr, target) << endl;

    return 0;
}
```

Output:

```text
4
```

---

# 33. Correct Recursive Program

```cpp
#include <iostream>
#include <vector>

using namespace std;

int recursiveBinarySearch(
    const vector<int>& arr,
    int target,
    int st,
    int end
) {

    if(st > end) {
        return -1;
    }

    int mid = st + (end - st) / 2;

    if(target > arr[mid]) {

        return recursiveBinarySearch(
            arr,
            target,
            mid + 1,
            end
        );
    }

    else if(target < arr[mid]) {

        return recursiveBinarySearch(
            arr,
            target,
            st,
            mid - 1
        );
    }

    else {

        return mid;
    }
}

int main() {

    vector<int> arr = {1, 2, 3, 4, 7, 44};

    int target = 7;

    int result = recursiveBinarySearch(
        arr,
        target,
        0,
        arr.size() - 1
    );

    cout << result << endl;

    return 0;
}
```

Output:

```text
4
```

---

# 34. Common Mistakes

## Mistake 1 — Using an Unsorted Array

Wrong:

```text
[1,5,2,8,3]
```

Binary search cannot safely operate on this.

Correct:

```text
[1,2,3,5,8]
```

---

## Mistake 2 — Wrong Mid Formula

Avoid:

```cpp
mid = (st + end) / 2;
```

Prefer:

```cpp
mid = st + (end - st) / 2;
```

---

## Mistake 3 — Wrong Direction

For ascending array:

```cpp
if(target > arr[mid])
    st = mid + 1;
```

and:

```cpp
if(target < arr[mid])
    end = mid - 1;
```

Do not reverse these conditions.

---

## Mistake 4 — Forgetting `+1`

Wrong:

```cpp
st = mid;
```

Correct:

```cpp
st = mid + 1;
```

because `mid` has already been checked.

---

## Mistake 5 — Forgetting `-1`

Wrong:

```cpp
end = mid;
```

Correct:

```cpp
end = mid - 1;
```

because `mid` has already been checked.

---

## Mistake 6 — Using `<` Instead of `<=`

Wrong for this standard implementation:

```cpp
while(st < end)
```

Correct:

```cpp
while(st <= end)
```

The case:

```text
st == end
```

still contains one candidate.

---

## Mistake 7 — Missing Recursive Base Case

Without:

```cpp
if(st > end)
    return -1;
```

the recursion may continue indefinitely.

---

# 35. Binary Search on Descending Arrays

Binary search can also work on descending arrays.

Example:

```text
9 8 7 6 5 4 3
```

But the movement rules change.

For ascending:

```text
target > arr[mid] → right
target < arr[mid] → left
```

For descending:

```text
target > arr[mid] → left
target < arr[mid] → right
```

The important thing is that the direction depends on the array's ordering.

---

# 36. Binary Search Is a Pattern, Not Just a Function

The deeper idea is:

> **Maintain a search space and repeatedly eliminate a portion of it using a monotonic condition.**

Standard binary search uses:

```text
sorted array
```

But the same thinking appears in many advanced problems.

Examples:

```text
First occurrence
Last occurrence
Lower bound
Upper bound
Search insert position
Peak element
Rotated sorted array
Binary search on answer
Minimum feasible value
Maximum feasible value
```

---

# 37. First Occurrence

Suppose:

```text
arr = [1,2,2,2,3,4]
```

Target:

```text
2
```

There are multiple answers:

```text
index 1
index 2
index 3
```

If the problem asks for the **first occurrence**, finding any `2` is not enough.

When:

```cpp
arr[mid] == target
```

store:

```cpp
ans = mid;
```

and continue searching left:

```cpp
end = mid - 1;
```

---

# 38. Last Occurrence

For:

```text
[1,2,2,2,3,4]
```

target:

```text
2
```

last occurrence is:

```text
index 3
```

When found:

```cpp
ans = mid;
```

continue right:

```cpp
st = mid + 1;
```

---

# 39. Search Insert Position

Example:

```text
arr = [1,3,5,6]
target = 5
```

Answer:

```text
2
```

If:

```text
target = 2
```

answer:

```text
1
```

because `2` should be inserted before `3`.

This is a classic binary-search problem.

---

# 40. Lower Bound Concept

For a sorted array, the lower bound of `target` is the first position where:

```text
arr[index] >= target
```

Example:

```text
arr = [1,2,4,4,5,7]
target = 4
```

Lower bound:

```text
index 2
```

---

# 41. Upper Bound Concept

The upper bound is the first position where:

```text
arr[index] > target
```

Example:

```text
arr = [1,2,4,4,5,7]
target = 4
```

Upper bound:

```text
index 4
```

---

# 42. Binary Search on Answer

This is a very important advanced DSA pattern.

Sometimes we are not searching for an element.

Instead, we search for the smallest or largest value satisfying a condition.

Example idea:

```text
Can I complete the task using X?
```

If:

```text
X works
```

then larger values may also work.

This creates a monotonic condition:

```text
false false false true true true
```

We can binary search for the first `true`.

This is called:

```text
Binary Search on Answer
```

---

# 43. Monotonicity

Binary search requires some form of ordered/monotonic structure.

For a sorted array:

```text
1 2 3 4 5 6
```

the comparison behavior changes predictably.

For answer-space binary search:

```text
false false false true true true
```

Once the condition becomes true, it stays true.

That allows us to eliminate half the search space.

---

# 44. Binary Search Pattern Recognition

When you see:

```text
Sorted array
```

think:

```text
Binary Search
```

When you see:

```text
Find first position
```

think:

```text
Binary Search
```

When you see:

```text
Find last position
```

think:

```text
Binary Search
```

When you see:

```text
Minimum value that satisfies condition
```

think:

```text
Binary Search on Answer
```

When you see:

```text
Maximum feasible value
```

think:

```text
Binary Search on Answer
```

---

# 45. Binary Search Template

## Standard Ascending Search

```cpp
int binarySearch(const vector<int>& arr, int target) {

    int st = 0;
    int end = arr.size() - 1;

    while(st <= end) {

        int mid = st + (end - st) / 2;

        if(arr[mid] == target) {

            return mid;
        }

        else if(arr[mid] < target) {

            st = mid + 1;
        }

        else {

            end = mid - 1;
        }
    }

    return -1;
}
```

This is the version worth memorizing.

---

# 46. Standard Binary Search Flow

```text
START
  ↓
st = 0
end = n-1
  ↓
st <= end?
  ↓
YES
  ↓
calculate mid
  ↓
arr[mid] == target?
 ┌───────────────┐
YES             NO
 ↓                ↓
return mid      compare
                 ↓
       ┌─────────┴─────────┐
       ↓                   ↓
target > mid          target < mid
       ↓                   ↓
st = mid + 1         end = mid - 1
       └─────────┬─────────┘
                 ↓
             repeat
                 ↓
           st > end
                 ↓
              return -1
```

---

# 47. Interview Explanation

A strong explanation:

> "Binary search works on sorted data. I maintain a search range using `st` and `end`. At each iteration, I calculate the middle index using `st + (end - st) / 2` to avoid potential integer overflow. If the target is greater than the middle element, I discard the left half by setting `st = mid + 1`. If the target is smaller, I discard the right half using `end = mid - 1`. If they are equal, I return the index. Since the search space is halved at every iteration, the time complexity is O(log n)."

---

# 48. Interview Questions

### Q1

Why does binary search require sorted data?

---

### Q2

Why is binary search O(log n)?

---

### Q3

Why use:

```cpp
st + (end - st)/2
```

instead of:

```cpp
(st + end)/2
```

?

---

### Q4

Why is the condition:

```cpp
st <= end
```

instead of:

```cpp
st < end
```

?

---

### Q5

Why do we use:

```cpp
mid + 1
```

and:

```cpp
mid - 1
```

?

---

### Q6

What happens if the target does not exist?

---

### Q7

What is the difference between iterative and recursive binary search?

---

### Q8

What is the extra space complexity of recursive binary search?

---

### Q9

Can binary search work on descending arrays?

---

### Q10

What is binary search on answer?

---

# 49. Practice Questions

## Beginner

1. Implement binary search iteratively.
2. Implement binary search recursively.
3. Find an element in a sorted array.
4. Return `-1` if the target is missing.
5. Count the number of iterations of binary search.

---

## Intermediate

6. Find first occurrence.
7. Find last occurrence.
8. Find total frequency of a target.
9. Search insert position.
10. Implement lower bound.
11. Implement upper bound.
12. Find floor of a number.
13. Find ceil of a number.

---

## Advanced

14. Search in rotated sorted array.
15. Find minimum in rotated sorted array.
16. Find peak element.
17. Find single element in a sorted array.
18. Search in a 2D matrix.
19. Find square root using binary search.
20. Binary Search on Answer problems.

---

# 50. Important LeetCode Problems

### Basic

**LeetCode 704 — Binary Search**

Classic binary search.

### Search Position

**LeetCode 35 — Search Insert Position**

### First / Last Position

**LeetCode 34 — Find First and Last Position of Element in Sorted Array**

### Rotated Array

**LeetCode 33 — Search in Rotated Sorted Array**

### Minimum Rotated Array

**LeetCode 153 — Find Minimum in Rotated Sorted Array**

### Peak

**LeetCode 162 — Find Peak Element**

### Matrix

**LeetCode 74 — Search a 2D Matrix**

These problems build the binary-search pattern progressively.

---

# 51. Complexity Summary

## Iterative

```text
Time:
O(log n)

Auxiliary Space:
O(1)
```

## Recursive

```text
Time:
O(log n)

Auxiliary Space:
O(log n)
```

because of the recursive call stack.

---

# 52. Binary Search vs Sorting

Do not confuse:

```text
Binary Search
```

with:

```text
Sorting
```

Binary search does **not** sort the array.

It assumes the search space already has the required ordering.

If you sort:

```cpp
sort(arr.begin(), arr.end());
```

the sorting operation itself costs:

```text
O(n log n)
```

Then binary search costs:

```text
O(log n)
```

---

# 53. Important Edge Cases

## Empty Array

```text
[]
```

There is nothing to search.

Return:

```text
-1
```

---

## One Element — Target Exists

```text
[5]
target = 5
```

Return:

```text
0
```

---

## One Element — Target Missing

```text
[5]
target = 10
```

Return:

```text
-1
```

---

## Target Smaller Than Everything

```text
[10,20,30,40]
target = 5
```

Eventually:

```text
end < st
```

Return:

```text
-1
```

---

## Target Greater Than Everything

```text
[10,20,30,40]
target = 50
```

Eventually:

```text
st > end
```

Return:

```text
-1
```

---

# 54. Duplicate Elements

Standard binary search can return **any matching index** when duplicates exist.

Example:

```text
[1,2,2,2,3]
```

Target:

```text
2
```

A standard binary search may return:

```text
1
```

or:

```text
2
```

or:

```text
3
```

depending on the midpoint progression.

If the problem asks for a specific occurrence, modify the algorithm.

---

# 55. ⭐ Most Important Binary Search Rules

```text
1. Data must be sorted for standard binary search.

2. Maintain:
   st = beginning
   end = ending

3. Calculate:
   mid = st + (end-st)/2

4. If target == arr[mid]:
   return mid

5. If target > arr[mid]:
   st = mid + 1

6. If target < arr[mid]:
   end = mid - 1

7. Continue while:
   st <= end

8. If the range becomes empty:
   return -1

9. Time:
   O(log n)

10. Iterative extra space:
    O(1)

11. Recursive extra space:
    O(log n)

12. For duplicate-specific problems:
    modify the search after finding a match.
```

---

# 56. 🧠 Final Mental Model

Think of binary search as a **detective eliminating impossible locations**.

Suppose:

```text
1 2 3 4 5 6 7 8 9
```

Target:

```text
8
```

Check middle:

```text
5
```

Since:

```text
8 > 5
```

everything on the left of `5` can be eliminated.

Remaining:

```text
6 7 8 9
```

Check middle again.

If:

```text
8 == 8
```

we found it.

The key is:

> **Never search where the target cannot possibly be.**

That is why binary search is fast.

---

# 57. ⭐ One-Line Memory Trick

> **"Sorted array → check middle → eliminate half → repeat → O(log n)."**

And remember the three decisions:

```text
target == arr[mid]
        ↓
      FOUND

target > arr[mid]
        ↓
   SEARCH RIGHT
   st = mid + 1

target < arr[mid]
        ↓
    SEARCH LEFT
   end = mid - 1
```

---

# 58. Final Code to Memorize

```cpp
#include <iostream>
#include <vector>

using namespace std;

int binarySearch(const vector<int>& arr, int target) {

    int st = 0;
    int end = arr.size() - 1;

    while(st <= end) {

        int mid = st + (end - st) / 2;

        if(arr[mid] == target) {

            return mid;
        }

        else if(arr[mid] < target) {

            st = mid + 1;
        }

        else {

            end = mid - 1;
        }
    }

    return -1;
}
```

### Complexity

```text
Time  = O(log n)
Space = O(1)
```

This is the **core binary search template** you should be able to write from memory.
