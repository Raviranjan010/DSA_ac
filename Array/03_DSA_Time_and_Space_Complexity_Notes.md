# 📘 DSA — Time & Space Complexity

## 1. What Is Time Complexity?

**Time Complexity** is the amount of computational work performed by an algorithm as a function of the input size `n`.

It does **not** mean the actual time in seconds.

Example:

```cpp
for(int i = 0; i < n; i++) {
    cout << i;
}
```

The loop runs `n` times:

```text
Time Complexity = O(n)
```

### Why don't we use actual seconds?

Actual execution time depends on:

- CPU
- RAM
- compiler
- compiler optimization
- operating system
- programming language
- machine load

Therefore, DSA focuses on **growth with input size**.

---

# 2. What Is `n`?

`n` generally represents the **input size**.

For an array:

```cpp
int arr[n];
```

```text
n = number of elements
```

For a string:

```text
n = length of string
```

For an `n × n` matrix:

```text
number of elements = n²
```

For a graph:

```text
V = number of vertices
E = number of edges
```

---

# 3. Big-O, Big-Omega and Big-Theta

A common shortcut is:

```text
Worst case  → O
Average case → Θ
Best case   → Ω
```

This is an oversimplification.

These notations describe **mathematical bounds**, while best/average/worst describe **cases**.

## Big-O — `O()`

Big-O represents an **asymptotic upper bound**.

In normal DSA discussions, Big-O is commonly used to state worst-case complexity.

Example:

```text
Linear Search
Worst Case → O(n)
```

## Big-Omega — `Ω()`

Omega represents an **asymptotic lower bound**.

Example:

```text
Linear Search
Best Case → Ω(1)
```

## Big-Theta — `Θ()`

Theta represents a **tight asymptotic bound**.

If an algorithm has both an `O(n)` upper bound and an `Ω(n)` lower bound, its tight bound is:

```text
Θ(n)
```

### Remember

```text
O(f(n))  → Upper Bound
Ω(f(n))  → Lower Bound
Θ(f(n))  → Tight Bound
```

Best, average, and worst case are separate forms of case analysis.

---

# 4. Space Complexity

**Space Complexity** is the amount of memory an algorithm requires as a function of input size `n`.

Example:

```cpp
int sum = 0;

for(int i = 0; i < n; i++) {
    sum += arr[i];
}
```

Only a few variables are used, so:

```text
Auxiliary Space = O(1)
```

## Auxiliary Space

Extra memory used by the algorithm apart from the input.

Example:

```cpp
vector<int> temp(n);
```

requires:

```text
Auxiliary Space = O(n)
```

---

# 5. Complexity Order

Generally:

```text
O(1)
    ↓
O(log n)
    ↓
O(n)
    ↓
O(n log n)
    ↓
O(n²)
    ↓
O(n³)
    ↓
O(2ⁿ)
    ↓
O(n!)
```

For large inputs, slower-growing complexity is generally more scalable.

---

# 6. O(1) — Constant Complexity

Example:

```cpp
int x = arr[5];
```

Accessing a known array index takes constant work:

```text
O(1)
```

It does not depend on the number of elements in the array.

---

# 7. O(n) — Linear Complexity

Example:

```cpp
for(int i = 0; i < n; i++) {
    cout << arr[i];
}
```

The loop executes:

```text
n times
```

Therefore:

```text
Time Complexity = O(n)
```

Common examples:

- Linear Search
- Kadane's Algorithm
- Moore's Voting Algorithm
- Two-pointer traversal
- Finding maximum/minimum

---

# 8. O(log n) — Logarithmic Complexity

Binary Search is the classic example.

Suppose:

```text
n = 16
```

The search space becomes:

```text
16
↓
8
↓
4
↓
2
↓
1
```

Number of steps:

```text
4
```

And:

```text
log₂(16) = 4
```

Therefore:

```text
Binary Search = O(log n)
```

---

# 9. Binary Search Derivation

Initially:

```text
n
```

After one iteration:

```text
n / 2
```

After two:

```text
n / 2²
```

After `x` iterations:

```text
n / 2ˣ
```

Eventually:

```text
n / 2ˣ = 1
```

Therefore:

```text
n = 2ˣ
```

Taking log base 2:

```text
log₂(n) = x
```

So:

```text
x = log₂(n)
```

Hence:

```text
Binary Search = O(log n)
```

---

# 10. Correct Binary Search Code

```cpp
int s = 0;
int e = n - 1;

while(s <= e) {

    int mid = s + (e - s) / 2;

    if(arr[mid] < target) {
        s = mid + 1;
    }

    else if(arr[mid] > target) {
        e = mid - 1;
    }

    else {
        return mid;
    }
}

return -1;
```

## Important Correction

Incorrect:

```cpp
if(arr[mid] < target) {
    s = mid - 1;
}
```

Correct:

```cpp
s = mid + 1;
```

### Why?

If:

```text
arr[mid] < target
```

the target must be to the **right** of `mid`.

Therefore:

```text
left = mid + 1
```

If:

```text
arr[mid] > target
```

the target must be to the **left**:

```text
right = mid - 1
```

### Requirement

Classic binary search requires a **sorted array**.

---

# 11. Factorial

Mathematically:

```text
n! = n × (n-1) × (n-2) × ... × 1
```

Example:

```text
5! = 5 × 4 × 3 × 2 × 1
   = 120
```

## Iterative Factorial

```cpp
int fact = 1;

for(int i = 1; i <= n; i++) {
    fact *= i;
}
```

The loop executes `n` times.

Therefore:

```text
Time Complexity = O(n)
```

### Very Important Distinction

The **result** grows as:

```text
n!
```

but the **algorithm** performs:

```text
n iterations
```

Therefore:

```text
Factorial value       → n!
Iterative calculation → O(n)
```

Do not confuse mathematical output growth with algorithmic running time.

---

# 12. Fibonacci Using Dynamic Programming

Fibonacci sequence:

```text
0 1 1 2 3 5 8 13 21 ...
```

Formula:

```text
F(n) = F(n-1) + F(n-2)
```

DP implementation:

```cpp
vector<int> dp(n + 1);

dp[0] = 0;
dp[1] = 1;

for(int i = 2; i <= n; i++) {
    dp[i] = dp[i-1] + dp[i-2];
}
```

The loop executes approximately `n` times:

```text
Time = O(n)
```

The DP array stores `n + 1` values:

```text
Space = O(n)
```

---

# 13. Fibonacci Space Optimization

To calculate the next Fibonacci value, we only need the previous two values.

```cpp
int prev2 = 0;
int prev1 = 1;

for(int i = 2; i <= n; i++) {

    int curr = prev1 + prev2;

    prev2 = prev1;
    prev1 = curr;
}
```

Complexity:

```text
Time  = O(n)
Space = O(1)
```

This is an important example of **space optimization in DP**.

---

# 14. Kadane's Algorithm

## Problem

Find the maximum sum of a **contiguous subarray**.

Example:

```text
[-2, 3, -1, 5, -6]
```

Best subarray:

```text
[3, -1, 5]
```

Sum:

```text
7
```

---

# 15. Kadane's Code

```cpp
int currSum = 0;
int ans = INT_MIN;

for(int i = 0; i < n; i++) {

    currSum += arr[i];

    ans = max(currSum, ans);

    currSum = currSum < 0 ? 0 : currSum;
}
```

Complexity:

```text
Time  = O(n)
Space = O(1)
```

---

# 16. Why Does Kadane Reset a Negative Sum?

Suppose:

```text
currSum = -10
```

and the next element is:

```text
20
```

Continuing:

```text
-10 + 20 = 10
```

Starting fresh:

```text
20
```

is better.

Therefore, when:

```text
currSum < 0
```

we discard the previous prefix:

```cpp
currSum = 0;
```

### Core idea

```text
Negative prefix
      ↓
Hurts future sum
      ↓
Discard it
      ↓
Start fresh
```

---

# 17. Kadane Edge Case

Consider:

```text
[-5, -2, -8]
```

Maximum non-empty subarray:

```text
[-2]
```

Answer:

```text
-2
```

not:

```text
0
```

Therefore:

```cpp
ans = INT_MIN;
```

is important in the standard implementation when the subarray must be non-empty.

---

# 18. Bubble Sort

## Definition

Bubble Sort repeatedly compares **adjacent elements** and swaps them if they are in the wrong order.

Example:

```text
5 3 4 1
```

Compare:

```text
5 and 3
```

Swap:

```text
3 5 4 1
```

Then:

```text
5 and 4
```

Swap:

```text
3 4 5 1
```

Then:

```text
5 and 1
```

Swap:

```text
3 4 1 5
```

The largest element has moved to the end.

---

# 19. Bubble Sort Code

```cpp
for(int i = 0; i < n - 1; i++) {

    for(int j = 0; j < n - i - 1; j++) {

        if(arr[j] > arr[j + 1]) {
            swap(arr[j], arr[j + 1]);
        }
    }
}
```

---

# 20. Bubble Sort Complexity Derivation

Suppose:

```text
n = 4
```

Pass 1:

```text
3 comparisons
```

Pass 2:

```text
2 comparisons
```

Pass 3:

```text
1 comparison
```

Total:

```text
3 + 2 + 1 = 6
```

For general `n`:

```text
(n-1) + (n-2) + ... + 2 + 1
```

Using:

```text
1 + 2 + ... + k = k(k+1)/2
```

with:

```text
k = n - 1
```

we get:

```text
n(n-1)/2
```

Expand:

```text
(n² - n)/2
```

Ignore the constant:

```text
n² - n
```

The dominant term is:

```text
n²
```

Therefore:

```text
Bubble Sort = O(n²)
```

---

# 21. Important Correction

A common incorrect conclusion is:

```text
n² - n ≈ n
```

Therefore:

```text
O(n)
```

This is wrong.

For large `n`, `n²` dominates `n`.

Example:

```text
n = 1000

n² = 1,000,000
n  = 1,000
```

Therefore:

```text
n² - n = O(n²)
```

---

# 22. Bubble Sort Complexity

For the basic implementation:

```text
Best Case    = O(n²)
Average Case = O(n²)
Worst Case   = O(n²)
Space        = O(1)
```

Why is the basic best case still `O(n²)`?

Because the nested loops continue making comparisons even when the array is already sorted.

---

# 23. Optimized Bubble Sort

We can stop early if no swap happens.

```cpp
for(int i = 0; i < n - 1; i++) {

    bool swapped = false;

    for(int j = 0; j < n - i - 1; j++) {

        if(arr[j] > arr[j + 1]) {

            swap(arr[j], arr[j + 1]);

            swapped = true;
        }
    }

    if(!swapped)
        break;
}
```

Now:

```text
Best Case    = O(n)
Average Case = O(n²)
Worst Case   = O(n²)
```

---

# 24. Selection Sort

## Definition

Selection Sort repeatedly finds the **minimum element** from the unsorted portion and places it at the current position.

Example:

```text
5 3 4 1
```

Find minimum:

```text
1
```

Swap with first position:

```text
1 3 4 5
```

Continue with the remaining unsorted portion.

---

# 25. Selection Sort Code

```cpp
for(int i = 0; i < n - 1; i++) {

    int minIdx = i;

    for(int j = i + 1; j < n; j++) {

        if(arr[j] < arr[minIdx]) {
            minIdx = j;
        }
    }

    swap(arr[i], arr[minIdx]);
}
```

---

# 26. Selection Sort Complexity Derivation

For:

```text
n = 5
```

When `i = 0`:

```text
4 comparisons
```

When `i = 1`:

```text
3 comparisons
```

Then:

```text
2
1
```

Total:

```text
4 + 3 + 2 + 1
```

General:

```text
(n-1) + (n-2) + ... + 1
```

Using:

```text
n(n-1)/2
```

Therefore:

```text
Selection Sort = O(n²)
```

---

# 27. Selection Sort Complexity

Standard Selection Sort:

```text
Best Case    = O(n²)
Average Case = O(n²)
Worst Case   = O(n²)
Space        = O(1)
```

Even if the array is already sorted, the algorithm still scans the remaining unsorted portion.

---

# 28. Bubble Sort vs Selection Sort

| Feature | Bubble Sort | Selection Sort |
|---|---|---|
| Main idea | Swap adjacent elements | Select minimum |
| Best basic | O(n²) | O(n²) |
| Best optimized Bubble | O(n) | O(n²) |
| Average | O(n²) | O(n²) |
| Worst | O(n²) | O(n²) |
| Extra space | O(1) | O(1) |
| Stable | Yes | Usually no |
| In-place | Yes | Yes |

---

# 29. Common Loop Patterns

## Linear Loop

```cpp
for(int i = 0; i < n; i++)
```

```text
O(n)
```

## Nested Linear Loops

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
    }
}
```

```text
O(n²)
```

## Triple Nested Loops

```cpp
for(int i = 0; i < n; i++)
    for(int j = 0; j < n; j++)
        for(int k = 0; k < n; k++)
```

```text
O(n³)
```

## Doubling

```cpp
for(int i = 1; i < n; i *= 2)
```

```text
O(log n)
```

## Halving

```cpp
for(int i = n; i > 0; i /= 2)
```

```text
O(log n)
```

---

# 30. Sequential vs Nested Loops

## Sequential

```cpp
for(int i = 0; i < n; i++) {
}

for(int i = 0; i < n; i++) {
}
```

Work:

```text
n + n
= 2n
= O(n)
```

## Nested

```cpp
for(int i = 0; i < n; i++) {

    for(int j = 0; j < n; j++) {
    }
}
```

Work:

```text
n × n
= n²
= O(n²)
```

### Mental Rule

```text
Sequential → Add
Nested     → Multiply
```

This is a useful starting rule, but always inspect the actual bounds.

---

# 31. Different Input Sizes

```cpp
for(int i = 0; i < n; i++) {

    for(int j = 0; j < m; j++) {
    }
}
```

Complexity:

```text
O(nm)
```

Not automatically:

```text
O(n²)
```

unless:

```text
m = n
```

---

# 32. Constant Inner Loop

```cpp
for(int i = 0; i < n; i++) {

    for(int j = 0; j < 10; j++) {
    }
}
```

Work:

```text
10n
```

Drop the constant:

```text
O(n)
```

---

# 33. Removing Constants

Suppose:

```text
T(n) = 5n² + 3n + 10
```

The dominant term is:

```text
n²
```

Therefore:

```text
O(n²)
```

---

# 34. Removing Lower-Order Terms

Suppose:

```text
T(n) = n² + 5n + 20
```

For large `n`, `n²` dominates.

Therefore:

```text
O(n²)
```

---

# 35. Complexity Cheat Sheet

| Complexity | Example |
|---|---|
| O(1) | Array access |
| O(log n) | Binary Search |
| O(n) | Linear Search |
| O(n) | Kadane |
| O(n) | Moore Voting |
| O(n) | Two Pointer |
| O(n log n) | Merge Sort |
| O(n²) | Bubble Sort |
| O(n²) | Selection Sort |
| O(n³) | Three nested loops |
| O(2ⁿ) | Naive recursive Fibonacci |
| O(n!) | Permutation brute force |

---

# 36. Common Mistakes

## Mistake 1

Thinking:

```text
Factorial result = n!
Therefore algorithm = O(n!)
```

Wrong.

```text
Iterative factorial = O(n)
```

---

## Mistake 2

Thinking:

```text
n² - n ≈ n
```

Wrong.

```text
n² - n = O(n²)
```

---

## Mistake 3

Thinking:

```text
Θ = average case
```

Wrong.

Theta means:

```text
tight asymptotic bound
```

---

## Mistake 4

Using:

```cpp
s = mid - 1;
```

when:

```text
arr[mid] < target
```

Correct:

```cpp
s = mid + 1;
```

---

## Mistake 5

Thinking every three-loop program is `O(n³)`.

Always inspect the actual loop limits.

---

# 37. Complexity Analysis Checklist

When given code:

### Step 1
Identify what `n` represents.

### Step 2
Count how many times each loop executes.

### Step 3
Check how loop variables change:

```text
i++
i--
i *= 2
i /= 2
```

### Step 4
Determine whether loops are:

```text
Sequential
```

or:

```text
Nested
```

### Step 5
Add sequential work.

### Step 6
Multiply nested work.

### Step 7
Remove constants.

### Step 8
Remove lower-order terms.

### Step 9
Keep the dominant term.

### Step 10
Analyze extra memory separately.

---

# 38. Practice Questions

## Basic

### Q1
Find the complexity:

```cpp
for(int i = 0; i < n; i++) {
}
```

Answer:

```text
O(n)
```

### Q2

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
    }
}
```

Answer:

```text
O(n²)
```

### Q3

```cpp
for(int i = 1; i < n; i *= 2) {
}
```

Answer:

```text
O(log n)
```

### Q4

```cpp
for(int i = 0; i < n; i++) {
}

for(int i = 0; i < n; i++) {
}
```

Answer:

```text
O(n)
```

because:

```text
O(n) + O(n)
= O(2n)
= O(n)
```

### Q5

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < i; j++) {
    }
}
```

Total work:

```text
0 + 1 + 2 + ... + (n-1)
```

Therefore:

```text
O(n²)
```

---

# 39. Intermediate Questions

1. Derive the number of comparisons in Bubble Sort.
2. Explain why Selection Sort is `O(n²)` even when the array is sorted.
3. Explain why Binary Search is `O(log n)`.
4. Explain the difference between `O`, `Ω`, and `Θ`.
5. Explain the difference between best, average, and worst case.
6. Find time and space complexity of Fibonacci DP.
7. Optimize Fibonacci space from `O(n)` to `O(1)`.
8. Explain why Kadane's Algorithm works.
9. Find complexity:

```cpp
for(int i = 1; i < n; i *= 2)
    for(int j = 0; j < n; j++) {
    }
```

Answer:

```text
O(n log n)
```

10. Find complexity:

```cpp
for(int i = 0; i < n; i++)
    for(int j = 1; j < n; j *= 2) {
    }
```

Answer:

```text
O(n log n)
```

---

# 40. Interview Questions

1. What is Time Complexity?
2. What is Space Complexity?
3. What is Big-O?
4. What is Big-Omega?
5. What is Big-Theta?
6. Are Big-O and worst case exactly the same concept?
7. Why do we ignore constants?
8. Why do we ignore lower-order terms?
9. Why is Binary Search `O(log n)`?
10. Why is Bubble Sort `O(n²)`?
11. Why is Selection Sort `O(n²)`?
12. Why is iterative factorial `O(n)`?
13. Why is naive recursive Fibonacci exponential?
14. How does DP improve Fibonacci?
15. How can Fibonacci space be reduced from `O(n)` to `O(1)`?
16. Why does Kadane use `O(1)` extra space?
17. What is the difference between input and auxiliary space?
18. What is the complexity of nested loops with bounds `n` and `m`?
19. What happens when a loop variable doubles each iteration?
20. How do you analyze mixed sequential and nested loops?

---

# 41. Must-Know Takeaways

```text
Time Complexity
→ Growth of computational work

Space Complexity
→ Growth of memory usage

O
→ Upper asymptotic bound

Ω
→ Lower asymptotic bound

Θ
→ Tight asymptotic bound

Factorial loop
→ O(n)

Fibonacci DP
→ O(n) time
→ O(n) space
→ O(1) space with optimization

Kadane
→ O(n) time
→ O(1) extra space

Binary Search
→ O(log n)
→ Sorted data required

Bubble Sort
→ O(n²) basic
→ O(n) best with early-exit optimization

Selection Sort
→ O(n²)

Sequential work
→ Add

Nested work
→ Multiply

Loop ×2 / ÷2
→ Usually O(log n)

n² - n
→ O(n²)

Dominant term
→ Determines asymptotic growth
```

---

# 42. Final Mental Model

```text
Given Code
    ↓
Identify n
    ↓
Analyze every loop
    ↓
How does the variable change?
    ├── +1 / -1 → usually linear
    ├── ×2 / ÷2 → usually logarithmic
    └── nested   → multiply work
    ↓
Sequential sections → add
    ↓
Write mathematical expression
    ↓
Remove constants
    ↓
Remove lower-order terms
    ↓
Keep dominant term
    ↓
Final Time Complexity
    ↓
Analyze extra memory
    ↓
Final Space Complexity
```

> **Core DSA skill:** Never classify complexity from the number of loops alone. Analyze how many times each loop actually executes. A single loop can be `O(log n)`, two nested loops can be `O(n log n)`, and a three-level-looking structure can still be `O(n²)` if one loop is constant-sized.
