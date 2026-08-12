# 📘 DSA Notes: Container With Most Water

LeetCode 11 — Container With Most Water

## 1. Problem Statement

Given an array of heights, choose two lines that form a container with the x-axis and contain the maximum possible amount of water.

Example:

```cpp
height = {1,8,6,2,5,4,8,3,7}
```

The answer is:

```text
49
```

---

# 2. Area Formula

If we choose indices `i` and `j`:

```text
width = j - i
height = min(height[i], height[j])
```

Therefore:

```text
Area = (j - i) × min(height[i], height[j])
```

### ⭐ Most Important Formula

```text
Water = width × minimum height
```

The shorter line determines how high the water can rise.

---

# 3. Why Minimum Height?

Suppose:

```text
left  = 8
right = 5
```

The water can only reach height `5`.

Therefore:

```text
height = min(8,5)
       = 5
```

We cannot use `8` because water would overflow over the shorter wall.

---

# 4. Brute Force Approach

Try every possible pair.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int maxArea(vector<int> height) {

    int maxWater = 0;

    for(int i = 0; i < height.size(); i++) {

        for(int j = i + 1; j < height.size(); j++) {

            int w = j - i;

            int h = min(height[i], height[j]);

            int currWater = w * h;

            maxWater = max(maxWater, currWater);
        }
    }

    return maxWater;
}
```

## How it works

For every pair:

```text
1. Calculate width
2. Find the shorter line
3. Calculate area
4. Update maximum area
```

## Complexity

```text
Time  = O(n²)
Space = O(1)
```

The problem is that for large `n`, checking every pair is too slow.

---

# 5. Two Pointer Approach

Initialize:

```cpp
int lp = 0;
int rp = height.size() - 1;
```

So:

```text
lp → leftmost line
rp → rightmost line
```

Example:

```text
lp                       rp
 ↓                        ↓
[1,8,6,2,5,4,8,3,7]
```

At every step:

```cpp
int w = rp - lp;
int h = min(height[lp], height[rp]);

int currWater = w * h;

maxWater = max(maxWater, currWater);
```

---

# 6. The Most Important Question

After calculating the area:

> Which pointer should move?

Rule:

```text
If left height < right height:
    move left pointer

Otherwise:
    move right pointer
```

In code:

```cpp
if(height[lp] < height[rp]) {
    lp++;
}
else {
    rp--;
}
```

---

# 7. Why Do We Move the Smaller Pointer?

This is the most important concept in the problem.

Area is:

```text
Area = width × min(leftHeight, rightHeight)
```

Suppose:

```text
left  = 3
right = 9
```

The limiting height is:

```text
3
```

Now suppose we move the right pointer.

The width becomes smaller, but the left wall is still `3`.

Therefore, the height cannot become greater than `3` because the left wall remains the bottleneck.

So moving the taller wall cannot produce a better area with the current shorter wall.

Instead, we move the shorter wall and search for a taller wall.

### ⭐ Core Rule

```text
Shorter wall = bottleneck
Bottleneck pointer = move it
```

---

# 8. Correct Two Pointer Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int maxArea(vector<int>& height) {

    int maxWater = 0;

    int lp = 0;
    int rp = height.size() - 1;

    while(lp < rp) {

        int w = rp - lp;

        int h = min(height[lp], height[rp]);

        int currWater = w * h;

        maxWater = max(maxWater, currWater);

        if(height[lp] < height[rp]) {
            lp++;
        }
        else {
            rp--;
        }
    }

    return maxWater;
}
```

---

# 9. Your Original Code — Correction

You wrote:

```cpp
rp = height.size()-1;
```

You must declare the variable:

```cpp
int rp = height.size() - 1;
```

You also wrote:

```cpp
height[lp] < height[rp] ? lp++ : rp--;
```

This is valid C++, but while learning, the clearer version is:

```cpp
if(height[lp] < height[rp]) {
    lp++;
}
else {
    rp--;
}
```

The ternary version is equivalent:

```cpp
height[lp] < height[rp] ? lp++ : rp--;
```

---

# 10. Dry Run

Input:

```text
height = [1,8,6,2,5,4,8,3,7]
```

Initial:

```text
lp = 0
rp = 8
```

## Iteration 1

```text
height[lp] = 1
height[rp] = 7
```

Width:

```text
8 - 0 = 8
```

Height:

```text
min(1,7) = 1
```

Area:

```text
8 × 1 = 8
```

Maximum:

```text
8
```

Since:

```text
1 < 7
```

move:

```text
lp++
```

---

## Iteration 2

Now:

```text
lp = 1
rp = 8
```

Heights:

```text
8 and 7
```

Width:

```text
8 - 1 = 7
```

Height:

```text
min(8,7) = 7
```

Area:

```text
7 × 7 = 49
```

Update:

```text
maxWater = 49
```

Since:

```text
7 < 8
```

move:

```text
rp--
```

---

## Iteration 3

```text
lp = 1
rp = 7
```

Heights:

```text
8 and 3
```

Width:

```text
7 - 1 = 6
```

Height:

```text
3
```

Area:

```text
6 × 3 = 18
```

Maximum remains:

```text
49
```

Since:

```text
3 < 8
```

move:

```text
rp--
```

The process continues until:

```text
lp >= rp
```

Final answer:

```text
49
```

---

# 11. Why Two Pointers Are O(n)

Initially:

```text
lp = 0
rp = n - 1
```

At every iteration, at least one pointer moves.

Neither pointer ever moves backward.

Therefore, the total number of pointer movements is at most proportional to `n`.

So:

```text
Time Complexity = O(n)
```

Only a few variables are used:

```text
lp
rp
w
h
currWater
maxWater
```

Therefore:

```text
Space Complexity = O(1)
```

---

# 12. Brute Force vs Two Pointer

| Feature | Brute Force | Two Pointer |
|---|---|---|
| Technique | Check every pair | Shrink search space |
| Time | O(n²) | O(n) |
| Space | O(1) | O(1) |
| Main idea | Exhaustive search | Eliminate impossible pairs |
| Interview importance | Basic | ⭐ Very Important |

---

# 13. Why Not Move the Taller Pointer?

Suppose:

```text
left = 4
right = 9
```

Current height:

```text
4
```

If we move the right pointer:

```text
right → right - 1
```

then:

```text
width decreases
```

while the left wall is still:

```text
4
```

So the height is still at most `4`.

Therefore, the new area cannot be better than the current area based on this same left wall.

We need to move the shorter wall:

```text
left++
```

and hope to find a taller wall.

---

# 14. Why Not Move Both Pointers?

Do not do:

```cpp
lp++;
rp--;
```

simultaneously.

Moving both can skip valid candidate pairs.

The reasoning only allows us to eliminate the side with the smaller height.

Therefore:

```text
Move exactly one pointer.
```

---

# 15. What If Both Heights Are Equal?

Suppose:

```text
height[lp] = height[rp]
```

Either pointer can be moved.

Example:

```cpp
if(height[lp] < height[rp])
    lp++;
else
    rp--;
```

When they are equal, the `else` moves `rp`.

That is valid.

---

# 16. Common Mistakes

## Mistake 1 — Using Maximum Height

Wrong:

```cpp
int h = max(height[lp], height[rp]);
```

Correct:

```cpp
int h = min(height[lp], height[rp]);
```

The shorter wall limits the water.

---

## Mistake 2 — Wrong Width

Wrong:

```cpp
int w = rp + lp;
```

Correct:

```cpp
int w = rp - lp;
```

Width is the distance between the two indices.

---

## Mistake 3 — Moving the Taller Pointer

Wrong logic:

```text
left = 3
right = 9

Move right
```

Correct:

```text
Move left
```

because `3` is the bottleneck.

---

## Mistake 4 — Moving Both Pointers

Wrong:

```cpp
lp++;
rp--;
```

Correct:

```cpp
if(height[lp] < height[rp])
    lp++;
else
    rp--;
```

---

## Mistake 5 — Forgetting `lp < rp`

Use:

```cpp
while(lp < rp)
```

When:

```text
lp == rp
```

there is only one line and:

```text
width = 0
```

so it cannot form a container.

---

# 17. Connection With Pair Sum

You previously learned Pair Sum using Two Pointers.

### Pair Sum

```text
sum < target
→ move left

sum > target
→ move right
```

because the array is sorted.

### Container With Most Water

```text
left height < right height
→ move left

right height < left height
→ move right
```

because the shorter height limits the area.

The deeper lesson is:

> Two pointers are useful when you can logically eliminate part of the search space.

---

# 18. Pattern Recognition

When you see:

> Maximum area between two lines

Think:

```text
Container With Most Water
        ↓
Area = width × minimum height
        ↓
Brute Force = O(n²)
        ↓
Need optimization
        ↓
Two Pointers
        ↓
Move smaller height
        ↓
O(n)
```

---

# 19. Interview Explanation

A strong interview explanation:

> "I use two pointers, one at the beginning and one at the end. For each pair, the area is `(right-left) * min(height[left], height[right])`. The shorter line limits the amount of water. Since moving the taller line only decreases the width while the current shorter line remains the limiting factor, it cannot improve the area. Therefore, I move the pointer at the shorter line. Each pointer moves only inward, so the time complexity is O(n) and the extra space is O(1)."

---

# 20. Practice Questions

### Q1

```text
height = [1,1]
```

Answer:

```text
1
```

---

### Q2

```text
height = [4,3,2,1,4]
```

Best pair:

```text
index 0 and index 4
```

Width:

```text
4
```

Height:

```text
4
```

Area:

```text
16
```

Answer:

```text
16
```

---

### Q3

```text
height = [1,2,1]
```

Best pair:

```text
index 0 and index 2
```

Area:

```text
2 × 1 = 2
```

Answer:

```text
2
```

---

### Q4

Dry-run:

```text
height = [3,8,1,5,7,2]
```

Track:

```text
lp
rp
width
height
area
maxWater
```

---

### Q5

Explain:

> Why can't we move the taller pointer?

---

### Q6

Explain:

> Why does moving the shorter pointer make sense even though it reduces the width?

---

# 21. Final Cheat Sheet

## Formula

```text
Area = width × height
```

where:

```text
width = right - left

height = min(height[left], height[right])
```

## Brute Force

```text
Try every pair

Time  = O(n²)
Space = O(1)
```

## Two Pointer

```cpp
int lp = 0;
int rp = height.size() - 1;

while(lp < rp) {

    int w = rp - lp;

    int h = min(height[lp], height[rp]);

    int currWater = w * h;

    maxWater = max(maxWater, currWater);

    if(height[lp] < height[rp])
        lp++;
    else
        rp--;
}
```

Complexity:

```text
Time  = O(n)
Space = O(1)
```

---

# 🧠 Core Concept

```text
             Area
               ↓
       width × height
               ↓
    width = right - left
               ↓
height = min(left, right)
               ↓
      Shorter wall = bottleneck
               ↓
       Move shorter pointer
               ↓
      Search for taller wall
               ↓
             O(n)
```

## ⭐ One-Line Memory Trick

> **"The shorter wall is the bottleneck, so move the shorter pointer."**
