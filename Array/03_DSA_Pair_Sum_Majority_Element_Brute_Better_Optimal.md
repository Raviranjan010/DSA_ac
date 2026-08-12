# 📘 DSA Notes: Pair Sum & Majority Element
## Brute → Better → Optimal

---

# 1️⃣ Pair Sum — Two Pointer Approach

## Problem Statement

Given a **sorted array** and a **target sum**, find two elements whose sum equals the target.

### Example

```cpp
nums = {2, 3, 4, 7, 8}
target = 12
```

We need:

```text
4 + 8 = 12
```

Indices:

```text
[2, 4]
```

---

## Why Is This Problem Important?

Pair Sum is one of the most important array problems because it teaches:

- Two Pointer Technique
- Array Traversal Optimization
- Time Complexity Reduction
- How sorted arrays can be exploited
- Brute Force → Optimal thinking
- Interview problem-solving patterns

---

# 2️⃣ Brute Force Approach

## Idea

Check every possible pair.

```cpp
for(int i = 0; i < n; i++) {

    for(int j = i + 1; j < n; j++) {

        if(nums[i] + nums[j] == target) {
            return {i, j};
        }
    }
}
```

---

## Example

```text
2 3 4 7 8
```

Target:

```text
12
```

We check:

```text
2 + 3
2 + 4
2 + 7
2 + 8
3 + 4
3 + 7
3 + 8
4 + 7
4 + 8  ✔
```

Therefore:

```text
Answer = [2, 4]
```

---

## Why Do We Start `j` from `i + 1`?

We don't want to use the same element twice.

For example:

```text
i = 2
j = 2
```

would mean:

```text
nums[2] + nums[2]
```

which is usually not allowed when the problem asks for two different indices.

We also don't need both:

```text
(i, j)
(j, i)
```

because they represent the same pair.

Therefore:

```cpp
j = i + 1;
```

---

## Brute Force Complexity

```text
Time  : O(n²)
Space : O(1)
```

### Why O(n²)?

There are nested loops:

```text
Loop 1 → n
Loop 2 → approximately n
```

Therefore:

```text
n × n = O(n²)
```

---

# 3️⃣ Optimal Approach — Two Pointers

## Core Condition

The array must be **sorted**.

Example:

```text
2 3 4 7 8
```

Because the elements are arranged in increasing order, we can intelligently decide which pointer to move.

---

# 4️⃣ Two Pointer Setup

Use two pointers:

```cpp
int i = 0;
int j = n - 1;
```

Conceptually:

```text
2   3   4   7   8
↑               ↑
i               j
```

Where:

```text
i = left pointer
j = right pointer
```

---

# 5️⃣ Calculate the Pair Sum

```cpp
int sum = nums[i] + nums[j];
```

Then there are three cases.

---

## Case 1 — `sum > target`

Example:

```text
target = 12

8 + 7 = 15
```

The sum is too large.

We need a smaller sum.

Because the array is sorted:

```text
2 3 4 7 8
        ↑
```

Moving the right pointer left gives us a smaller value.

Therefore:

```cpp
j--;
```

### Rule

```text
sum > target
      ↓
Need smaller sum
      ↓
Move right pointer left
      ↓
j--
```

---

# 6️⃣ Case 2 — `sum < target`

Example:

```text
2 + 8 = 10
```

Target:

```text
12
```

The sum is too small.

We need a bigger sum.

Because the array is sorted, moving the left pointer right gives us a larger value.

Therefore:

```cpp
i++;
```

### Rule

```text
sum < target
      ↓
Need bigger sum
      ↓
Move left pointer right
      ↓
i++
```

---

# 7️⃣ Case 3 — `sum == target`

Example:

```text
4 + 8 = 12
```

Target found.

Therefore:

```cpp
return {i, j};
```

---

# 8️⃣ Two Pointer Dry Run

### Input

```text
nums = {2, 3, 4, 7, 8}
target = 12
```

---

## Iteration 1

Pointers:

```text
2 3 4 7 8
↑       ↑
i       j
```

Calculate:

```text
2 + 8 = 10
```

Since:

```text
10 < 12
```

move:

```text
i++
```

Now:

```text
i = 1
j = 4
```

---

## Iteration 2

```text
2 3 4 7 8
  ↑     ↑
  i     j
```

Calculate:

```text
3 + 8 = 11
```

Since:

```text
11 < 12
```

move:

```text
i++
```

---

## Iteration 3

```text
2 3 4 7 8
    ↑   ↑
    i   j
```

Calculate:

```text
4 + 8 = 12
```

Therefore:

```text
sum == target
```

Answer:

```text
indices = [2, 4]
```

---

# 9️⃣ Complete Two Pointer Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> pairSum(const vector<int>& nums, int target) {

    int i = 0;
    int j = nums.size() - 1;

    while(i < j) {

        int sum = nums[i] + nums[j];

        if(sum > target) {
            j--;
        }

        else if(sum < target) {
            i++;
        }

        else {
            return {i, j};
        }
    }

    return {};
}

int main() {

    vector<int> nums = {2, 3, 4, 7, 8};
    int target = 12;

    vector<int> ans = pairSum(nums, target);

    if(!ans.empty()) {
        cout << ans[0] << " " << ans[1] << endl;
    }

    return 0;
}
```

### Output

```text
2 4
```

---

# 🔟 Why Does Two Pointer Work?

Suppose:

```text
2 3 4 7 8
```

and:

```text
2 + 8 = 10
```

Target:

```text
12
```

We need a bigger sum.

Could we move `8`?

No.

The values to the left of `8` are smaller:

```text
2 3 4 7 8
        ↑
```

Moving the right pointer left would make the sum even smaller.

Therefore, the only useful move is:

```text
i++
```

Similarly, if:

```text
7 + 8 = 15
```

is too large, moving `i` right would make the sum larger.

So the useful move is:

```text
j--
```

This is exactly why the sorted property is important.

---

# 1️⃣1️⃣ Complexity

| Approach | Time | Extra Space |
|---|---:|---:|
| Brute Force | O(n²) | O(1) |
| Two Pointers | O(n) | O(1) |

The two-pointer approach reduces:

```text
O(n²)
```

to:

```text
O(n)
```

---

# 1️⃣2️⃣ Important Condition

The simple two-pointer Pair Sum algorithm requires a **sorted array**.

This will work:

```text
1 2 3 4 5 6
```

This is not directly suitable:

```text
4 1 6 2 5 3
```

because moving the pointers no longer guarantees that the sum will increase or decrease in the required direction.

---

# 1️⃣3️⃣ Pair Sum on an Unsorted Array

If the array is unsorted, a common optimal approach is **hashing**.

Example:

```text
nums = [2, 7, 11, 15]
target = 9
```

For every number, calculate:

```text
needed = target - current
```

For:

```text
current = 2
needed = 9 - 2 = 7
```

Store `2`.

Next:

```text
current = 7
needed = 9 - 7 = 2
```

`2` has already been seen.

Therefore:

```text
2 + 7 = 9
```

---

# 1️⃣4️⃣ Pair Sum — Hashing Code

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

vector<int> twoSum(const vector<int>& nums, int target) {

    unordered_map<int, int> mp;

    for(int i = 0; i < nums.size(); i++) {

        int needed = target - nums[i];

        if(mp.count(needed)) {
            return {mp[needed], i};
        }

        mp[nums[i]] = i;
    }

    return {};
}
```

Complexity:

```text
Average Time : O(n)
Space        : O(n)
```

---

# 1️⃣5️⃣ Pair Sum — Three Main Approaches

| Approach | Requirement | Time | Space |
|---|---|---:|---:|
| Brute Force | Any array | O(n²) | O(1) |
| Two Pointers | Sorted array | O(n) | O(1) |
| Hashing | Any array | O(n) average | O(n) |

---

# 1️⃣6️⃣ Interview Questions Related to Pair Sum

### LeetCode 1 — Two Sum

Find two indices whose values add to the target.

### LeetCode 167 — Two Sum II

Two Sum on a sorted array.

### LeetCode 15 — 3Sum

Find triplets whose sum is zero.

### LeetCode 18 — 4Sum

Find quadruplets whose sum equals a target.

### LeetCode 11 — Container With Most Water

Uses the two-pointer pattern, but for a different mathematical objective.

### LeetCode 26 — Remove Duplicates from Sorted Array

Uses sorted-array and two-pointer thinking.

### LeetCode 283 — Move Zeroes

Uses two-pointer/in-place array manipulation.

---

# 1️⃣7️⃣ Majority Element

## LeetCode 169

---

# 1️⃣8️⃣ Problem Statement

Find the element that appears more than:

```text
n / 2
```

times in the array.

Example:

```text
nums = [2, 2, 1, 1, 1, 2, 2]
```

Array size:

```text
n = 7
```

Frequency:

```text
2 → 4 times
1 → 3 times
```

Majority condition:

```text
frequency > n/2
```

Therefore:

```text
4 > 7/2
4 > 3
```

So:

```text
Answer = 2
```

---

# 1️⃣9️⃣ Important Observation

There can be only **one** majority element.

Why?

Suppose:

```text
n = 10
```

If `A` appears more than half:

```text
A > 5
```

and `B` also appears more than half:

```text
B > 5
```

Then:

```text
A + B > 10
```

But the array contains only 10 elements.

Impossible.

Therefore:

> At most one element can be a majority element.

---

# 2️⃣0️⃣ Important Definition: Strictly More Than Half

Majority means:

```text
frequency > n/2
```

NOT:

```text
frequency >= n/2
```

For:

```text
n = 6
```

an element must occur at least:

```text
4 times
```

because:

```text
4 > 3
```

But:

```text
3 > 3
```

is false.

---

# 2️⃣1️⃣ Approach 1 — Brute Force

## Idea

For every element:

1. Count its frequency.
2. Check whether frequency is greater than `n/2`.
3. Return it if found.

---

## Code

```cpp
class Solution {
public:

    int majorityElement(vector<int>& nums) {

        int n = nums.size();

        for(int val : nums) {

            int freq = 0;

            for(int el : nums) {

                if(el == val) {
                    freq++;
                }
            }

            if(freq > n / 2) {
                return val;
            }
        }

        return -1;
    }
};
```

---

# 2️⃣2️⃣ Brute Force Dry Run

Array:

```text
[2, 2, 1, 1, 1, 2, 2]
```

Take:

```text
val = 2
```

Count all occurrences:

```text
2 → count 1
2 → count 2
1 → ignore
1 → ignore
1 → ignore
2 → count 3
2 → count 4
```

Therefore:

```text
freq = 4
```

Since:

```text
4 > 7/2
```

return:

```text
2
```

---

# 2️⃣3️⃣ Brute Force Complexity

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
Time = O(n²)
```

Extra variables:

```text
Space = O(1)
```

---

# 2️⃣4️⃣ Approach 2 — Sorting

## Core Idea

After sorting, equal elements become adjacent.

Before:

```text
2 2 1 1 1 2 2
```

After sorting:

```text
1 1 1 2 2 2 2
```

Now the majority element is grouped together.

---

# 2️⃣5️⃣ Sorting Code

```cpp
class Solution {
public:

    int majorityElement(vector<int>& nums) {

        sort(nums.begin(), nums.end());

        int n = nums.size();

        int freq = 1;
        int ans = nums[0];

        for(int i = 1; i < n; i++) {

            if(nums[i] == nums[i - 1]) {
                freq++;
            }

            else {
                freq = 1;
                ans = nums[i];
            }

            if(freq > n / 2) {
                return ans;
            }
        }

        return ans;
    }
};
```

### Required Header

```cpp
#include <algorithm>
```

for:

```cpp
sort()
```

---

# 2️⃣6️⃣ Simpler Sorting Trick

If the problem guarantees that a majority element exists, there is a much simpler observation.

After sorting:

```text
1 1 1 2 2 2 2
```

The middle element is:

```text
index = n / 2
```

Therefore:

```cpp
sort(nums.begin(), nums.end());

return nums[nums.size() / 2];
```

---

# 2️⃣7️⃣ Why Does the Middle Element Work?

A majority element occurs more than half the time.

Therefore, after sorting, its block is large enough to cross the middle position.

Example:

```text
1 1 1 2 2 2 2
```

Middle:

```text
index = 7 / 2 = 3
```

```text
nums[3] = 2
```

Therefore:

```text
majority = 2
```

---

# 2️⃣8️⃣ Sorting Complexity

Sorting:

```text
O(n log n)
```

Then accessing the middle:

```text
O(1)
```

Therefore:

```text
Time = O(n log n)
```

The exact extra-space behavior depends on the sorting implementation, so do not blindly claim O(1) auxiliary space for every standard-library implementation.

---

# 2️⃣9️⃣ Approach 3 — Hash Map

## Idea

Store the frequency of every element.

Example:

```text
2 → 4
1 → 3
```

Then return the element whose frequency becomes greater than:

```text
n/2
```

---

# 3️⃣0️⃣ Hash Map Code

```cpp
class Solution {
public:

    int majorityElement(vector<int>& nums) {

        unordered_map<int, int> mp;

        int n = nums.size();

        for(int x : nums) {

            mp[x]++;

            if(mp[x] > n / 2) {
                return x;
            }
        }

        return -1;
    }
};
```

Required header:

```cpp
#include <unordered_map>
```

---

# 3️⃣1️⃣ Hash Map Complexity

Average expected:

```text
Time = O(n)
Space = O(n)
```

Why O(n) space?

In the worst case, many distinct values may be stored in the hash map.

---

# 3️⃣2️⃣ Approach 4 — Moore's Voting Algorithm

## ⭐ BEST INTERVIEW APPROACH

Moore's Voting Algorithm is also called the:

> **Boyer-Moore Majority Vote Algorithm**

It finds the majority candidate in:

```text
Time  = O(n)
Space = O(1)
```

when a majority element is guaranteed to exist.

---

# 3️⃣3️⃣ Intuition

Think of:

```text
Majority Element = Hero
Other Elements   = Villains
```

Whenever:

```text
Hero + Villain
```

meet, they cancel each other.

Because the majority element appears more than half the time, it has more "votes" than all other elements combined.

After cancellation, the majority element survives.

---

# 3️⃣4️⃣ Core Variables

We maintain:

```cpp
int candidate;
int count;
```

Meaning:

```text
candidate → current possible majority
count     → current vote balance
```

---

# 3️⃣5️⃣ Moore's Voting Rules

## Rule 1 — Count becomes zero

Choose a new candidate:

```cpp
if(count == 0) {
    candidate = nums[i];
}
```

---

## Rule 2 — Current value equals candidate

Increase count:

```cpp
if(nums[i] == candidate) {
    count++;
}
```

---

## Rule 3 — Current value differs

Decrease count:

```cpp
else {
    count--;
}
```

---

# 3️⃣6️⃣ Moore's Voting Code

```cpp
class Solution {
public:

    int majorityElement(vector<int>& nums) {

        int count = 0;
        int candidate = 0;

        for(int i = 0; i < nums.size(); i++) {

            if(count == 0) {
                candidate = nums[i];
            }

            if(candidate == nums[i]) {
                count++;
            }

            else {
                count--;
            }
        }

        return candidate;
    }
};
```

---

# 3️⃣7️⃣ Moore's Voting Dry Run

Input:

```text
[2, 2, 1, 1, 1, 2, 2]
```

---

## Start

```text
candidate = ?
count = 0
```

### Element = 2

Count is zero.

Choose:

```text
candidate = 2
```

Same:

```text
count = 1
```

---

### Element = 2

Same candidate:

```text
count = 2
```

---

### Element = 1

Different:

```text
count = 1
```

---

### Element = 1

Different:

```text
count = 0
```

---

### Element = 1

Count is zero.

Choose new candidate:

```text
candidate = 1
```

Then:

```text
count = 1
```

---

### Element = 2

Different:

```text
count = 0
```

---

### Element = 2

Count is zero.

Choose:

```text
candidate = 2
```

Then:

```text
count = 1
```

Final:

```text
candidate = 2
```

Answer:

```text
2
```

---

# 3️⃣8️⃣ Why Moore's Voting Works

Suppose the majority element appears:

```text
> n/2
```

times.

All non-majority elements together occur fewer than the majority element.

We can repeatedly cancel:

```text
majority element
      +
different element
```

Each cancellation removes one majority occurrence and one non-majority occurrence.

Since majority occurrences are more numerous, they cannot all be canceled.

Therefore, the final candidate is the majority element.

---

# 3️⃣9️⃣ Very Important: Candidate vs Verified Answer

Moore's first phase gives us a **candidate**.

If the problem guarantees:

```text
A majority element always exists
```

then the candidate can be returned directly.

But if a majority is **not guaranteed**, we must verify it.

Example:

```text
[1, 2, 3]
```

No element occurs more than:

```text
3/2 = 1
```

times.

So there is no majority.

---

# 4️⃣0️⃣ Moore's Voting with Verification

```cpp
class Solution {
public:

    int majorityElement(vector<int>& nums) {

        int count = 0;
        int candidate = 0;

        // Phase 1: Find candidate
        for(int x : nums) {

            if(count == 0) {
                candidate = x;
            }

            if(x == candidate) {
                count++;
            }
            else {
                count--;
            }
        }

        // Phase 2: Verify candidate
        int freq = 0;

        for(int x : nums) {

            if(x == candidate) {
                freq++;
            }
        }

        if(freq > nums.size() / 2) {
            return candidate;
        }

        return -1;
    }
};
```

Complexity:

```text
Time  = O(n)
Space = O(1)
```

Even with verification, the total is:

```text
O(n) + O(n)
= O(n)
```

---

# 4️⃣1️⃣ Majority Element Comparison

| Approach | Time | Extra Space | Main Idea |
|---|---:|---:|---|
| Brute Force | O(n²) | O(1) | Count every element |
| Sorting | O(n log n) | Depends | Group equal elements |
| Hash Map | O(n) average | O(n) | Store frequencies |
| Moore's Voting | O(n) | O(1) | Cancel different elements |

---

# 4️⃣2️⃣ Which Approach Should You Choose?

### If learning the problem for the first time

Start with:

```text
Brute Force
```

because it teaches the direct logic.

Then improve to:

```text
Sorting
```

Then:

```text
Hash Map
```

Finally master:

```text
Moore's Voting
```

---

# 4️⃣3️⃣ Pattern Recognition

If you see:

> "Find Majority Element"

Think:

```text
Brute Force
     ↓
Frequency Count
     ↓
Sorting
     ↓
Hash Map
     ↓
Moore's Voting
```

If the interviewer asks:

> Can you do it in O(n) time and O(1) space?

Think immediately:

```text
Moore's Voting Algorithm
```

---

# 4️⃣4️⃣ Pair Sum Pattern Recognition

If you see:

> "Find two numbers whose sum equals target"

Ask:

```text
Is the array sorted?
```

### Yes

Think:

```text
Two Pointers
```

### No

Think:

```text
Hash Map
```

### Constraints are very small

Brute force may be acceptable:

```text
O(n²)
```

---

# 4️⃣5️⃣ Related Problems

## LeetCode 169

**Majority Element**

```text
frequency > n/2
```

Uses:

```text
Moore's Voting
```

---

## LeetCode 229

**Majority Element II**

Find elements appearing more than:

```text
n/3
```

This uses a modified form of Moore's Voting Algorithm with multiple candidates.

---

## LeetCode 1

**Two Sum**

General Pair Sum problem.

---

## LeetCode 167

**Two Sum II — Input Array Is Sorted**

Excellent two-pointer problem.

---

## LeetCode 15

**3Sum**

Builds on sorting + two pointers.

---

## LeetCode 18

**4Sum**

Extends the idea further.

---

## LeetCode 26

**Remove Duplicates from Sorted Array**

Two-pointer technique.

---

## LeetCode 283

**Move Zeroes**

Two-pointer/in-place array manipulation.

---

## LeetCode 11

**Container With Most Water**

Another important two-pointer problem.

---

# 4️⃣6️⃣ Common Mistakes — Pair Sum

### Mistake 1

Using two pointers on an unsorted array.

```text
Wrong assumption:
Any array → two pointers
```

Correct:

```text
Sorted array → two-pointer logic
```

---

### Mistake 2

Moving the wrong pointer.

If:

```text
sum > target
```

move:

```text
right--
```

If:

```text
sum < target
```

move:

```text
left++
```

---

### Mistake 3

Using:

```cpp
while(i <= j)
```

when two distinct elements are required.

Usually:

```cpp
while(i < j)
```

is correct.

---

### Mistake 4

Ignoring the possibility that no pair exists.

Return:

```cpp
{}
```

and check:

```cpp
if(!ans.empty())
```

before accessing:

```cpp
ans[0]
ans[1]
```

---

# 4️⃣7️⃣ Common Mistakes — Majority Element

### Mistake 1

Using:

```text
>= n/2
```

instead of:

```text
> n/2
```

---

### Mistake 2

Forgetting that Moore's candidate may need verification if majority existence is not guaranteed.

---

### Mistake 3

Thinking:

```text
final candidate = always majority
```

without checking the problem constraints.

---

### Mistake 4

Confusing:

```text
n/2
```

with:

```text
ceil(n/2)
```

The definition is specifically:

```text
frequency > n/2
```

---

# 4️⃣8️⃣ Interview Questions

## Pair Sum

### Q1. Why does two-pointer Pair Sum require a sorted array?

### Q2. Why do we move `i` when sum is too small?

### Q3. Why do we move `j` when sum is too large?

### Q4. Why is brute force O(n²)?

### Q5. Why is two-pointer O(n)?

### Q6. Can two pointers be used directly on an unsorted array?

### Q7. How can hashing solve Pair Sum?

### Q8. What is the space complexity of hashing?

### Q9. What is the difference between Two Sum and Two Sum II?

### Q10. What changes when solving 3Sum?

---

# 4️⃣9️⃣ Interview Questions — Majority Element

### Q11. What is a majority element?

### Q12. Why can there be at most one majority element?

### Q13. What is the brute-force complexity?

### Q14. How does sorting help?

### Q15. Why can `nums[n/2]` be the majority after sorting?

### Q16. What is the complexity of sorting?

### Q17. How does a hash map solve the problem?

### Q18. What is Moore's Voting Algorithm?

### Q19. Why does cancellation work?

### Q20. What is the difference between a candidate and a verified majority?

### Q21. What happens if there is no majority?

### Q22. How is Majority Element II different?

---

# 5️⃣0️⃣ Coding Practice Questions

## Beginner

### Q1. Find Pair Sum using brute force.

### Q2. Find Pair Sum using two pointers.

### Q3. Find Pair Sum using hashing.

### Q4. Return the pair values instead of indices.

### Q5. Count how many pairs produce the target.

---

## Intermediate

### Q6. Find the first Pair Sum in a sorted array.

### Q7. Find all unique pairs whose sum equals target.

### Q8. Solve Two Sum without using extra space when the array is sorted.

### Q9. Find the majority element using brute force.

### Q10. Find the majority element using sorting.

### Q11. Find the majority element using a hash map.

### Q12. Find the majority element using Moore's Voting Algorithm.

---

## Advanced

### Q13. Verify whether a Moore candidate is actually a majority.

### Q14. Solve Majority Element II (`> n/3`).

### Q15. Solve 3Sum.

### Q16. Solve 4Sum.

### Q17. Find all pairs with a given difference.

### Q18. Find the number of pairs with a given sum.

### Q19. Find the closest pair sum to a target.

### Q20. Find the pair with the maximum product.

---

# 5️⃣1️⃣ Master Decision Tree

```text
PAIR SUM
   │
   ├── Is array sorted?
   │       │
   │       ├── YES
   │       │    ↓
   │       │ Two Pointers
   │       │    ↓
   │       │ O(n) time
   │       │ O(1) extra space
   │       │
   │       └── NO
   │            ↓
   │         Hash Map
   │            ↓
   │         O(n) average
   │         O(n) space
   │
   └── Small constraints?
            ↓
         Brute Force
            ↓
         O(n²)
```

---

# 5️⃣2️⃣ Majority Element Decision Tree

```text
MAJORITY ELEMENT
       │
       ├── Learning basic idea
       │       ↓
       │   Brute Force
       │
       ├── Can modify/sort array?
       │       ↓
       │    Sorting
       │
       ├── Need O(n) time?
       │       ↓
       │    Hash Map
       │
       └── Need O(n) time + O(1) space?
               ↓
        Moore's Voting
```

---

# 5️⃣3️⃣ Final Interview Summary

## Pair Sum

```text
Problem:
Find two elements whose sum = target.

Sorted array:
→ Two Pointers
→ O(n) time
→ O(1) extra space
```

Core rules:

```text
sum > target
→ j--

sum < target
→ i++

sum == target
→ answer found
```

---

## Majority Element

```text
Problem:
Element appears more than n/2 times.
```

Approaches:

```text
Brute Force
→ O(n²)

Sorting
→ O(n log n)

Hash Map
→ O(n) average
→ O(n) space

Moore's Voting
→ O(n)
→ O(1) space
```

---

# 5️⃣4️⃣ Moore's Voting — Must Remember

```text
Same Element
      ↓
count++

Different Element
      ↓
count--

count == 0
      ↓
Choose New Candidate
```

Mental model:

```text
Majority = Hero
Different element = Opponent

Hero + Opponent
      ↓
Cancel each other

Majority has more votes
      ↓
Majority survives
```

---

# 5️⃣5️⃣ Final Cheat Sheet

```text
PAIR SUM
──────────────
Sorted → Two Pointers
Unsorted → Hashing
Brute → O(n²)
Two Pointer → O(n)
Hashing → O(n) average


MAJORITY ELEMENT
────────────────────────
Definition → freq > n/2

Brute Force → O(n²)
Sorting → O(n log n)
Hash Map → O(n) average, O(n) space
Moore → O(n), O(1)


TWO POINTER RULE
────────────────────────
sum > target → right--
sum < target → left++
sum == target → found


MOORE RULE
────────────────────────
same → count++
different → count--
count == 0 → new candidate


MOST IMPORTANT INTERVIEW PATTERNS
──────────────────────────────────
Sorted Array
    ↓
Two Pointers

Frequency
    ↓
Hashing / Counting

Majority > n/2
    ↓
Moore's Voting

Contiguous Maximum Sum
    ↓
Kadane's Algorithm
```

---

# 5️⃣6️⃣ What You Should Be Able to Explain Without Looking at Notes

Before considering this topic complete, you should be able to explain:

1. What Pair Sum is.
2. Why brute force is O(n²).
3. Why sorting enables two pointers.
4. Why `sum < target` means `left++`.
5. Why `sum > target` means `right--`.
6. Why two pointers are O(n).
7. How hashing solves Pair Sum on an unsorted array.
8. What a majority element means.
9. Why only one majority can exist.
10. How brute-force majority works.
11. How sorting can find the majority.
12. Why the middle element works after sorting when majority is guaranteed.
13. How frequency hashing works.
14. How Moore's Voting Algorithm works.
15. Why cancellation proves the majority candidate.
16. When Moore's candidate needs verification.
17. The difference between O(n) time/O(n) space and O(n) time/O(1) space.
18. Which approach to choose based on the array's properties and constraints.

> **DSA principle:** Do not jump directly to the optimal code. First understand the brute-force solution, identify the repeated work, exploit the input property (such as sorting), and then optimize. This is the real skill behind moving from **Brute → Better → Optimal**.
