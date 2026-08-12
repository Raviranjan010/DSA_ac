# 📘 DSA Notes: Product of Array Except Self

## LeetCode 238

**Problem:** Product of Array Except Self

https://leetcode.com/problems/product-of-array-except-self/description/

---

# 1. Problem Statement

Given an integer array:

```text
nums
```

return an array `ans` such that:

```text
ans[i] = product of every element except nums[i]
```

The product must contain all elements **except the element at index `i`**.

### Example

```text
nums = [1,2,3,4]
```

For index `0`:

```text
2 × 3 × 4 = 24
```

For index `1`:

```text
1 × 3 × 4 = 12
```

For index `2`:

```text
1 × 2 × 4 = 8
```

For index `3`:

```text
1 × 2 × 3 = 6
```

Therefore:

```text
Output = [24,12,8,6]
```

---

# 2. The Main Challenge

At first glance, the problem looks simple:

```text
For every index:
    multiply all other elements
```

But doing that directly causes repeated work.

We want to avoid repeatedly calculating the same products.

The important idea is:

```text
Product except nums[i]
=
product of elements to the LEFT
×
product of elements to the RIGHT
```

So:

```text
ans[i] = prefixProduct[i] × suffixProduct[i]
```

This is the key concept.

---

# 3. Brute Force Approach

For every index `i`, iterate through the entire array and multiply every element except `nums[i]`.

```cpp
class Solution {
public:

    vector<int> productExceptSelf(vector<int>& nums) {

        int n = nums.size();

        vector<int> ans(n, 1);

        for(int i = 0; i < n; i++) {

            for(int j = 0; j < n; j++) {

                if(i != j) {
                    ans[i] *= nums[j];
                }
            }
        }

        return ans;
    }
};
```

## How It Works

Suppose:

```text
nums = [1,2,3,4]
```

For:

```text
i = 0
```

we multiply:

```text
2 × 3 × 4 = 24
```

For:

```text
i = 1
```

we multiply:

```text
1 × 3 × 4 = 12
```

And so on.

---

# 4. Complexity of Brute Force

Outer loop:

```text
O(n)
```

Inner loop:

```text
O(n)
```

Therefore:

```text
O(n × n)
= O(n²)
```

Space:

```text
O(n)
```

because the answer array is required.

Therefore:

```text
Time  = O(n²)
Space = O(n)
```

### Important

If the problem asks for **extra space excluding the output array**, then the auxiliary space is:

```text
O(1)
```

But the returned `ans` array itself requires:

```text
O(n)
```

---

# 5. Why Brute Force Is Not Good Enough

Suppose:

```text
n = 1000
```

The brute-force approach performs approximately:

```text
1,000 × 1,000
= 1,000,000
```

operations.

For very large arrays, this becomes expensive.

We need to reuse previously calculated products.

---

# 6. Prefix and Suffix Product

For each index, divide the array into two parts:

```text
LEFT | CURRENT | RIGHT
```

We want:

```text
product of LEFT × product of RIGHT
```

We intentionally exclude:

```text
CURRENT
```

Therefore:

```text
ans[i] = leftProduct × rightProduct
```

---

# 7. Example

Consider:

```text
nums = [1,2,3,4]
```

For index `2`:

```text
1  2 | 3 | 4
```

Left product:

```text
1 × 2 = 2
```

Right product:

```text
4
```

Therefore:

```text
ans[2] = 2 × 4
       = 8
```

---

# 8. Method 2 — Separate Left and Right Arrays

We can explicitly store:

```text
left[i]
right[i]
```

where:

```text
left[i]  = product of elements before i
right[i] = product of elements after i
```

Then:

```text
ans[i] = left[i] × right[i]
```

---

# 9. Building the Left Array

Suppose:

```text
nums = [1,2,3,4]
```

Initialize:

```text
left = [1,1,1,1]
```

Why `1`?

Because `1` is the multiplicative identity:

```text
1 × x = x
```

Now:

```cpp
for(int i = 1; i < n; i++) {
    left[i] = left[i-1] * nums[i-1];
}
```

Let's calculate:

```text
left[1] = left[0] × nums[0]
        = 1 × 1
        = 1

left[2] = left[1] × nums[1]
        = 1 × 2
        = 2

left[3] = left[2] × nums[2]
        = 2 × 3
        = 6
```

Therefore:

```text
left = [1,1,2,6]
```

Notice:

```text
left[i]
```

does NOT include:

```text
nums[i]
```

---

# 10. Building the Right Array

Similarly:

```cpp
for(int i = n - 2; i >= 0; i--) {
    right[i] = right[i+1] * nums[i+1];
}
```

For:

```text
nums = [1,2,3,4]
```

Start:

```text
right = [1,1,1,1]
```

Calculate:

```text
right[2] = right[3] × nums[3]
         = 1 × 4
         = 4

right[1] = right[2] × nums[2]
         = 4 × 3
         = 12

right[0] = right[1] × nums[1]
         = 12 × 2
         = 24
```

Therefore:

```text
right = [24,12,4,1]
```

---

# 11. Combine Left and Right

Now:

```text
ans[i] = left[i] × right[i]
```

For:

```text
left  = [1,1,2,6]
right = [24,12,4,1]
```

we get:

```text
ans[0] = 1 × 24 = 24

ans[1] = 1 × 12 = 12

ans[2] = 2 × 4 = 8

ans[3] = 6 × 1 = 6
```

Final:

```text
[24,12,8,6]
```

---

# 12. Method 2 Code

```cpp
class Solution {
public:

    vector<int> productExceptSelf(vector<int>& nums) {

        int n = nums.size();

        vector<int> ans(n, 1);
        vector<int> left(n, 1);
        vector<int> right(n, 1);

        // Prefix products
        for(int i = 1; i < n; i++) {
            left[i] = left[i-1] * nums[i-1];
        }

        // Suffix products
        for(int i = n - 2; i >= 0; i--) {
            right[i] = right[i+1] * nums[i+1];
        }

        // Combine
        for(int i = 0; i < n; i++) {
            ans[i] = left[i] * right[i];
        }

        return ans;
    }
};
```

---

# 13. Correction in Your Method 2

You wrote:

```cpp
ans[i] = prefix[i] * suffix[i];
```

but your arrays were named:

```cpp
left
right
```

Therefore it should be:

```cpp
ans[i] = left[i] * right[i];
```

---

# 14. Complexity of Method 2

We perform three linear traversals:

```text
Left calculation  → O(n)
Right calculation → O(n)
Answer calculation → O(n)
```

Therefore:

```text
O(n) + O(n) + O(n)
= O(3n)
= O(n)
```

Space:

```text
left  → O(n)
right → O(n)
ans   → O(n)
```

Overall:

```text
Space = O(n)
```

---

# 15. Can We Optimize the Space?

Yes.

We don't actually need separate:

```text
left
right
```

arrays.

We can store the prefix product directly in:

```text
ans
```

Then use one variable:

```text
right
```

to maintain the suffix product.

This is the most important optimized approach.

---

# 16. Optimal Approach — Prefix in `ans`, Suffix in One Variable

First calculate the prefix products and store them in `ans`.

```cpp
for(int i = 1; i < n; i++) {
    ans[i] = ans[i-1] * nums[i-1];
}
```

After this:

```text
ans[i] = product of all elements before i
```

Then traverse from right to left.

Maintain:

```cpp
int right = 1;
```

At each index:

```cpp
right *= nums[i+1];
ans[i] *= right;
```

Now `ans[i]` becomes:

```text
prefix product × suffix product
```

---

# 17. Optimized Code

```cpp
class Solution {
public:

    vector<int> productExceptSelf(vector<int>& nums) {

        int n = nums.size();

        vector<int> ans(n, 1);

        // Prefix products
        for(int i = 1; i < n; i++) {
            ans[i] = ans[i-1] * nums[i-1];
        }

        // Suffix products
        int right = 1;

        for(int i = n - 2; i >= 0; i--) {

            right *= nums[i+1];

            ans[i] *= right;
        }

        return ans;
    }
};
```

---

# 18. Why Does `ans` Start With All 1s?

We create:

```cpp
vector<int> ans(n, 1);
```

because multiplication uses `1` as the identity.

For example:

```text
1 × 2 = 2
1 × 3 = 3
```

This makes the prefix calculation work naturally.

---

# 19. Detailed Dry Run of the Optimized Approach

Input:

```text
nums = [1,2,3,4]
```

Expected:

```text
[24,12,8,6]
```

---

# 20. Phase 1 — Build Prefix Products

Initially:

```text
ans = [1,1,1,1]
```

We execute:

```cpp
for(int i = 1; i < n; i++) {
    ans[i] = ans[i-1] * nums[i-1];
}
```

---

## i = 1

```text
ans[1] = ans[0] × nums[0]
       = 1 × 1
       = 1
```

Array:

```text
ans = [1,1,1,1]
```

---

## i = 2

```text
ans[2] = ans[1] × nums[1]
       = 1 × 2
       = 2
```

Array:

```text
ans = [1,1,2,1]
```

---

## i = 3

```text
ans[3] = ans[2] × nums[2]
       = 2 × 3
       = 6
```

Array:

```text
ans = [1,1,2,6]
```

### After Phase 1

```text
nums = [1,2,3,4]

ans  = [1,1,2,6]
```

Interpretation:

```text
ans[0] = product before index 0 = 1
ans[1] = product before index 1 = 1
ans[2] = product before index 2 = 1×2 = 2
ans[3] = product before index 3 = 1×2×3 = 6
```

So:

```text
ans = [1,1,2,6]
```

is currently the **prefix product array**.

---

# 21. Phase 2 — Build Suffix Product

Now:

```cpp
int right = 1;
```

Why?

Before index `n-1`, there are no elements to its right.

The empty product is treated as:

```text
1
```

We traverse:

```text
i = n-2
```

toward:

```text
0
```

---

# 22. i = 2

Current:

```text
nums[3] = 4
```

Update:

```cpp
right *= nums[i+1];
```

Therefore:

```text
right = 1 × 4
      = 4
```

Now:

```cpp
ans[i] *= right;
```

So:

```text
ans[2] = 2 × 4
       = 8
```

Array:

```text
ans = [1,1,8,6]
```

Interpretation:

```text
prefix = 1 × 2 = 2
suffix = 4
answer = 2 × 4 = 8
```

---

# 23. i = 1

Update:

```text
right = right × nums[2]
      = 4 × 3
      = 12
```

Then:

```text
ans[1] = 1 × 12
       = 12
```

Array:

```text
ans = [1,12,8,6]
```

Interpretation:

```text
prefix = 1
suffix = 3 × 4 = 12

answer = 1 × 12
       = 12
```

---

# 24. i = 0

Update:

```text
right = right × nums[1]
      = 12 × 2
      = 24
```

Then:

```text
ans[0] = 1 × 24
       = 24
```

Array:

```text
ans = [24,12,8,6]
```

Final answer:

```text
[24,12,8,6]
```

---

# 25. Complete Dry Run Table

For:

```text
nums = [1,2,3,4]
```

### Prefix Phase

| i | Calculation | `ans` |
|---:|---|---|
| Initial | — | `[1,1,1,1]` |
| 1 | `1 × 1 = 1` | `[1,1,1,1]` |
| 2 | `1 × 2 = 2` | `[1,1,2,1]` |
| 3 | `2 × 3 = 6` | `[1,1,2,6]` |

### Suffix Phase

| i | `right` calculation | `ans[i]` | `ans` |
|---:|---|---:|---|
| Initial | `right = 1` | — | `[1,1,2,6]` |
| 2 | `1 × 4 = 4` | `2 × 4 = 8` | `[1,1,8,6]` |
| 1 | `4 × 3 = 12` | `1 × 12 = 12` | `[1,12,8,6]` |
| 0 | `12 × 2 = 24` | `1 × 24 = 24` | `[24,12,8,6]` |

---

# 26. Why Does the Optimized Approach Work?

After the first loop:

```text
ans[i] = product of everything before i
```

Then `right` maintains:

```text
right = product of everything after i
```

Therefore:

```text
ans[i]
=
prefix product
×
suffix product
```

which is exactly:

```text
product of every element except nums[i]
```

---

# 27. Important Invariant

An **invariant** is a condition that remains true during an algorithm.

During the second loop:

> Before updating `ans[i]`, `right` represents the product of elements strictly to the right of index `i`.

Then:

```cpp
right *= nums[i+1];
```

updates `right` so it represents all elements from:

```text
i+1 → n-1
```

Then:

```cpp
ans[i] *= right;
```

combines:

```text
left product × right product
```

This gives the required answer.

---

# 28. Why Start the Second Loop at `n-2`?

We write:

```cpp
for(int i = n - 2; i >= 0; i--)
```

because:

```text
ans[n-1]
```

already contains the product of everything before it.

For the last element, there is nothing to its right.

Therefore its suffix product is:

```text
1
```

So:

```text
ans[n-1]
```

doesn't need to be multiplied by anything.

---

# 29. Why Use `nums[i+1]`?

At index:

```text
i
```

we want elements **after** `i`.

The immediate next element is:

```text
nums[i+1]
```

So:

```cpp
right *= nums[i+1];
```

adds the next element into the suffix product.

---

# 30. Why Doesn't the Optimized Approach Need Division?

A tempting solution is:

```text
totalProduct / nums[i]
```

For example:

```text
nums = [1,2,3,4]

total = 24

ans[0] = 24 / 1 = 24
ans[1] = 24 / 2 = 12
...
```

But this approach has a major problem:

## Zero

Consider:

```text
nums = [1,2,0,4]
```

Total product:

```text
0
```

Now:

```text
0 / nums[i]
```

cannot correctly solve every position.

The prefix/suffix approach naturally handles zeros without division.

---

# 31. Zero Example

Consider:

```text
nums = [1,2,0,4]
```

Correct output:

```text
[0,0,8,0]
```

Why?

For index `2`:

```text
1 × 2 × 4 = 8
```

For every other position, the product includes the zero:

```text
0
```

The prefix/suffix algorithm handles this automatically.

---

# 32. Multiple Zeros

Example:

```text
nums = [1,0,3,0]
```

Every product except one element still contains at least one zero.

Therefore:

```text
[0,0,0,0]
```

Again, no special division logic is required.

---

# 33. Complexity of Optimized Approach

First loop:

```text
O(n)
```

Second loop:

```text
O(n)
```

Total:

```text
O(n) + O(n)
= O(2n)
= O(n)
```

The answer array is required:

```text
O(n)
```

Extra variables:

```text
right
i
```

require:

```text
O(1)
```

Therefore, the standard interview complexity is:

```text
Time  = O(n)
Space = O(1) extra space
```

**Important:** The returned `ans` array itself takes `O(n)` memory. The `O(1)` claim refers to **auxiliary/extra space apart from the output array**.

---

# 34. Three Approaches Comparison

| Approach | Time | Extra Space | Main Idea |
|---|---:|---:|---|
| Brute Force | O(n²) | O(1)* | Multiply all other elements |
| Prefix + Suffix Arrays | O(n) | O(n) | Store left and right products |
| Optimized Prefix + Right Variable | O(n) | O(1)* | Reuse `ans` for prefix |

`*` Output array itself requires `O(n)`.

---

# 35. Pattern Recognition

When you see:

> Product of array except self

Think:

```text
Don't use division
        ↓
Split around current index
        ↓
LEFT × RIGHT
        ↓
Prefix product
+
Suffix product
        ↓
Store prefix in answer
        ↓
Maintain suffix with one variable
        ↓
O(n) time
O(1) extra space
```

---

# 36. Common Mistakes

## Mistake 1

Using:

```cpp
ans[i] = prefix[i] * suffix[i];
```

when arrays are actually named:

```cpp
left
right
```

Correct:

```cpp
ans[i] = left[i] * right[i];
```

---

## Mistake 2

Forgetting to return `ans`

Incorrect:

```cpp
vector<int> productExceptSelf(...) {
    ...
}
```

Correct:

```cpp
return ans;
```

---

## Mistake 3

Starting prefix from `0`

Wrong:

```cpp
for(int i = 0; i < n; i++)
```

for the standard prefix calculation.

Correct:

```cpp
for(int i = 1; i < n; i++) {
    ans[i] = ans[i-1] * nums[i-1];
}
```

---

## Mistake 4

Including `nums[i]` in the prefix

Wrong:

```cpp
ans[i] = ans[i-1] * nums[i];
```

Correct:

```cpp
ans[i] = ans[i-1] * nums[i-1];
```

The prefix must stop **before** index `i`.

---

## Mistake 5

Including `nums[i]` in the suffix

The suffix should begin from:

```text
i + 1
```

not:

```text
i
```

That's why:

```cpp
right *= nums[i+1];
```

---

## Mistake 6

Using division

```cpp
total / nums[i]
```

This fails when the array contains zero and is not the intended optimal approach for this problem.

---

# 37. Interview Explanation

A strong explanation:

> "For every index, the answer is the product of all elements to its left multiplied by the product of all elements to its right. First, I store the prefix product for every index directly in the answer array. Then I traverse from right to left while maintaining a single `right` product. I multiply `ans[i]` by this suffix product. This avoids the need for separate prefix and suffix arrays and gives O(n) time with O(1) auxiliary space, excluding the output array."

---

# 38. Core Code to Memorize

```cpp
class Solution {
public:

    vector<int> productExceptSelf(vector<int>& nums) {

        int n = nums.size();

        vector<int> ans(n, 1);

        // Prefix product
        for(int i = 1; i < n; i++) {
            ans[i] = ans[i-1] * nums[i-1];
        }

        // Suffix product
        int right = 1;

        for(int i = n - 2; i >= 0; i--) {

            right *= nums[i+1];

            ans[i] *= right;
        }

        return ans;
    }
};
```

---

# 39. ⭐ Mental Model

Imagine:

```text
nums = [1, 2, 3, 4]
```

For each position:

```text
[ LEFT ] [ SELF ] [ RIGHT ]
```

We need:

```text
LEFT × RIGHT
```

For example:

```text
1  2 | 3 | 4

LEFT  = 1×2 = 2
RIGHT = 4

answer = 2×4 = 8
```

The optimized algorithm does exactly this without creating separate arrays.

---

# 40. Final Cheat Sheet

```text
LeetCode 238
Product of Array Except Self
```

### Formula

```text
answer[i]
=
product(left side)
×
product(right side)
```

### Brute Force

```text
O(n²)
```

### Prefix + Suffix Arrays

```text
Time  = O(n)
Space = O(n)
```

### Optimized

```text
Prefix → store inside ans
Suffix → maintain in right
```

```cpp
for(int i = 1; i < n; i++) {
    ans[i] = ans[i-1] * nums[i-1];
}

int right = 1;

for(int i = n - 2; i >= 0; i--) {

    right *= nums[i+1];

    ans[i] *= right;
}
```

Complexity:

```text
Time       = O(n)
Extra Space = O(1)
Output      = O(n)
```

### ⭐ One-Line Memory Trick

> **"Build the left product inside `ans`, then multiply each position by the right product while scanning backward."**
