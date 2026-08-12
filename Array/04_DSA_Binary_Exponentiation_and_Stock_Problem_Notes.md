# 📘 DSA Notes: Binary Exponentiation & Best Time to Buy and Sell Stock

## 1. Binary Exponentiation / Fast Power

### Problem

Given `x` and `n`, calculate:

```text
xⁿ
```

Example:

```text
x = 2
n = 10

2¹⁰ = 1024
```

LeetCode: **Pow(x, n)** — LeetCode 50

---

## 2. Brute Force Power

The simplest approach repeatedly multiplies `x`:

```cpp
double ans = 1;

for(int i = 0; i < n; i++) {
    ans *= x;
}
```

For `x = 2, n = 10`, this performs approximately 10 multiplications.

```text
Time Complexity = O(n)
Space Complexity = O(1)
```

We can improve this to `O(log n)`.

---

# 3. Key Idea: Binary Representation

Binary Exponentiation represents the exponent in binary and uses repeated squaring.

### Important correction

```text
8 = 1000₂
```

not:

```text
8 = 10000₂
```

For example:

```text
13 = 1101₂
```

Therefore:

```text
13 = 8 + 4 + 1
```

So:

```text
x¹³ = x⁸ × x⁴ × x¹
```

This is the core idea behind fast power.

---

# 4. Repeated Squaring

Suppose:

```text
x = 2
```

We generate:

```text
x¹
x²
x⁴
x⁸
x¹⁶
x³²
...
```

For `x = 2`:

```text
2¹  = 2
2²  = 4
2⁴  = 16
2⁸  = 256
2¹⁶ = 65536
```

The exponent doubles each time, so only `O(log n)` iterations are needed.

---

# 5. Why `% 2`?

In C++:

```cpp
binForm % 2
```

checks whether the current exponent is odd or even.

Example:

```text
13 % 2 = 1
6  % 2 = 0
3  % 2 = 1
1  % 2 = 1
```

Therefore:

```cpp
if(binForm % 2 == 1)
```

means:

> The current binary bit is `1`, so multiply the answer by the current power of `x`.

---

# 6. Why `binForm /= 2`?

Integer division by 2 effectively removes the last binary bit.

Example:

```text
13 = 1101₂
```

Then:

```text
13 / 2 = 6  → 110₂
6  / 2 = 3  → 11₂
3  / 2 = 1  → 1₂
1  / 2 = 0
```

So the number of iterations is logarithmic:

```text
O(log n)
```

---

# 7. Important Correction in the Original Code

Incorrect:

```cpp
if(binForm % 2 == 1){
    ans += x;
}
```

Correct:

```cpp
if(binForm % 2 == 1){
    ans *= x;
}
```

We are calculating a product of powers, so multiplication is required.

---

# 8. Correct Binary Exponentiation Code

```cpp
#include <iostream>
using namespace std;

double myPow(double x, int n) {

    if(n == 0)
        return 1.0;

    if(x == 0)
        return 0.0;

    if(x == 1)
        return 1.0;

    long long binForm = n;

    if(binForm < 0) {
        x = 1 / x;
        binForm = -binForm;
    }

    double ans = 1.0;

    while(binForm > 0) {

        if(binForm % 2 == 1) {
            ans *= x;
        }

        x *= x;

        binForm /= 2;
    }

    return ans;
}
```

---

# 9. Why `long long`?

Using:

```cpp
long long binForm = n;
```

is safer than directly negating an `int`.

A 32-bit signed integer has:

```text
INT_MIN = -2147483648
```

Its positive counterpart:

```text
2147483648
```

cannot be represented by a signed 32-bit `int`.

Therefore, converting to `long long` before handling a negative exponent avoids the integer overflow problem for this algorithm.

---

# 10. Negative Exponents

Mathematical rule:

```text
x⁻ⁿ = 1 / xⁿ
```

Example:

```text
2⁻³ = 1 / 2³ = 1/8
```

Therefore:

```cpp
if(binForm < 0) {
    x = 1 / x;
    binForm = -binForm;
}
```

converts:

```text
x⁻ⁿ
```

into:

```text
(1/x)ⁿ
```

---

# 11. Dry Run: `2¹³`

Input:

```text
x = 2
n = 13
```

Initial:

```text
ans = 1
x = 2
binForm = 13
```

### Iteration 1

```text
13 % 2 = 1
```

Therefore:

```text
ans = 1 × 2 = 2
```

Square:

```text
x = 2² = 4
```

Divide:

```text
13 / 2 = 6
```

### Iteration 2

```text
6 % 2 = 0
```

Don't multiply.

Square:

```text
x = 4² = 16
```

Divide:

```text
6 / 2 = 3
```

### Iteration 3

```text
3 % 2 = 1
```

Multiply:

```text
ans = 2 × 16 = 32
```

Square:

```text
x = 16² = 256
```

Divide:

```text
3 / 2 = 1
```

### Iteration 4

```text
1 % 2 = 1
```

Multiply:

```text
ans = 32 × 256 = 8192
```

Divide:

```text
1 / 2 = 0
```

Stop.

Answer:

```text
8192
```

---

# 12. Binary Exponentiation Complexity

The exponent is repeatedly divided by 2:

```text
n
n/2
n/4
n/8
...
1
```

Therefore:

```text
Time Complexity = O(log n)
Space Complexity = O(1)
```

### Comparison

| Approach | Time | Space |
|---|---:|---:|
| Brute Force | O(n) | O(1) |
| Binary Exponentiation | O(log n) | O(1) |

---

# 13. Pattern Recognition — Binary Exponentiation

Whenever you see:

> Calculate `xⁿ`

Think:

```text
Power
↓
Binary representation of n
↓
Repeated squaring
↓
O(log n)
```

Core pattern:

```cpp
if(n % 2 == 1)
    ans *= x;

x *= x;
n /= 2;
```

---

# 14. Best Time to Buy and Sell Stock

LeetCode 121:

**Best Time to Buy and Sell Stock**

The goal is to make one buy and one later sell so that the profit is maximum.

---

# 15. Problem Statement

Given stock prices for different days:

```text
prices = [7,1,5,3,6,4]
```

You may:

1. Buy once.
2. Sell once.
3. Sell only after buying.
4. Maximize the profit.

Formula:

```text
Profit = Selling Price - Buying Price
```

Best transaction:

```text
Buy at 1
Sell at 6
```

Profit:

```text
6 - 1 = 5
```

Answer:

```text
5
```

---

# 16. Key Observation

For every day, imagine:

> **Today is the selling day.**

Then ask:

> What is the cheapest price at which I could have bought before today?

Maintain:

```text
bestBuy
```

which represents:

> Minimum stock price seen so far.

Then calculate:

```text
profit = current price - bestBuy
```

Maintain:

```text
maxProfit
```

which represents:

> Maximum valid profit found so far.

---

# 17. Optimal Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int maxProfit(vector<int>& prices) {

    int bestBuy = prices[0];
    int maxProfit = 0;

    for(int i = 1; i < prices.size(); i++) {

        bestBuy = min(bestBuy, prices[i]);

        maxProfit = max(
            maxProfit,
            prices[i] - bestBuy
        );
    }

    return maxProfit;
}
```

Complexity:

```text
Time  = O(n)
Space = O(1)
```

---

# 18. Why Does This Work?

For every selling day `i`, we want:

```text
prices[i] - prices[j]
```

where:

```text
j < i
```

Instead of checking every previous day, we maintain:

```text
minimum price seen so far
```

Therefore:

```text
Today's Profit
=
Today's Price
-
Minimum Previous Price
```

Then keep the maximum.

This converts an `O(n²)` pair-checking problem into an `O(n)` one-pass solution.

---

# 19. Dry Run

Input:

```text
prices = [7,1,5,3,6,4]
```

Initial:

```text
bestBuy = 7
maxProfit = 0
```

### Price = 1

```text
bestBuy = min(7,1)
        = 1

profit = 1 - 1
       = 0
```

```text
maxProfit = 0
```

### Price = 5

```text
bestBuy = 1

profit = 5 - 1
       = 4
```

```text
maxProfit = 4
```

### Price = 3

```text
profit = 3 - 1
       = 2
```

Maximum remains:

```text
4
```

### Price = 6

```text
profit = 6 - 1
       = 5
```

Update:

```text
maxProfit = 5
```

### Price = 4

```text
profit = 4 - 1
       = 3
```

Maximum remains:

```text
5
```

Final:

```text
Answer = 5
```

---

# 20. Your Original Code — What Can Be Improved?

You wrote:

```cpp
if(prices[i] > bestBuy){
    maxProfit = max(maxProfit, prices[i]-bestBuy);
}
else{
    bestBuy = prices[i];
}

bestBuy = min(bestBuy,prices[i]);
```

The final line:

```cpp
bestBuy = min(bestBuy, prices[i]);
```

already handles the minimum-price update.

Therefore, the `else` is unnecessary.

Simpler:

```cpp
for(int i = 1; i < prices.size(); i++) {

    bestBuy = min(bestBuy, prices[i]);

    maxProfit = max(
        maxProfit,
        prices[i] - bestBuy
    );
}
```

---

# 21. Brute Force Stock Solution

Try every possible buy/sell pair:

```cpp
int maxProfit(vector<int>& prices) {

    int maxProfit = 0;

    for(int i = 0; i < prices.size(); i++) {

        for(int j = i + 1; j < prices.size(); j++) {

            int profit = prices[j] - prices[i];

            maxProfit = max(maxProfit, profit);
        }
    }

    return maxProfit;
}
```

Complexity:

```text
Time  = O(n²)
Space = O(1)
```

---

# 22. Brute Force vs Optimal

| Approach | Idea | Time | Space |
|---|---|---:|---:|
| Brute Force | Try every buy/sell pair | O(n²) | O(1) |
| Optimal | Track minimum buy price | O(n) | O(1) |

---

# 23. Decreasing Prices

Example:

```text
prices = [7,6,4,3,1]
```

There is no profitable transaction.

Therefore:

```text
Answer = 0
```

Why?

Because we can simply choose not to trade.

That's why:

```cpp
int maxProfit = 0;
```

is correct.

---

# 24. One-Element Array

Example:

```text
prices = [5]
```

There is no valid buy-and-sell pair.

Answer:

```text
0
```

A defensive implementation can use:

```cpp
if(prices.empty())
    return 0;
```

For LeetCode's constraints, the array contains at least one element.

---

# 25. Common Mistakes

## Mistake 1 — Selling Before Buying

Invalid:

```text
Buy at day 5
Sell at day 2
```

The buying day must be earlier than the selling day.

Scanning left-to-right naturally maintains this condition.

---

## Mistake 2 — Using the Global Minimum Incorrectly

You cannot simply find the minimum and maximum independently.

The order matters.

You need:

```text
minimum price BEFORE current selling day
```

That's why we track:

```text
bestBuy
```

while scanning.

---

## Mistake 3 — Returning a Negative Profit

For:

```text
[7,6,5,4,3]
```

don't return:

```text
-1
```

The best choice is no transaction:

```text
0
```

---

# 26. Connection to Kadane's Algorithm

There is a useful conceptual connection.

For:

```text
prices = [7,1,5,3,6,4]
```

daily changes are:

```text
-6, +4, -2, +3, -2
```

The maximum stock profit can be viewed as the maximum sum of a contiguous sequence of these changes.

This is related to Kadane's Algorithm.

However, for LeetCode 121, the cleanest solution is:

```text
Minimum Buy Price
+
Maximum Profit
```

---

# 27. Pattern Recognition — Stock Problem

When you see:

> Buy once and sell later to maximize profit

Think:

```text
Stock Problem
      ↓
One transaction
      ↓
Minimum price so far
      ↓
Current price = selling price
      ↓
Current profit = price - minimum
      ↓
Maximum profit
      ↓
O(n)
```

---

# 28. Interview Cheat Sheet

## Binary Exponentiation

```text
Problem:
Calculate xⁿ

Brute Force:
O(n)

Optimal:
Binary Exponentiation

Time:
O(log n)

Space:
O(1)
```

Core:

```cpp
if(binForm % 2 == 1)
    ans *= x;

x *= x;
binForm /= 2;
```

---

## Best Time to Buy and Sell Stock

```text
Problem:
Maximum profit from one buy + one sell

Brute Force:
O(n²)

Optimal:
Track minimum price

Time:
O(n)

Space:
O(1)
```

Core:

```cpp
bestBuy = min(bestBuy, prices[i]);

maxProfit = max(
    maxProfit,
    prices[i] - bestBuy
);
```

---

# 29. Practice Questions

## Binary Exponentiation

1. Calculate `2¹⁰` using binary exponentiation.
2. Calculate `3¹³`.
3. Convert `25` into binary.
4. Explain why binary exponentiation is `O(log n)`.
5. Why do we use `n % 2`?
6. Why do we perform `x *= x`?
7. Why do we perform `n /= 2`?
8. How do negative exponents work?
9. What happens when `n = 0`?
10. Compare brute-force power with binary exponentiation.

## Stock Problem

11. Find the maximum profit:

```text
[7,1,5,3,6,4]
```

12. Find the maximum profit:

```text
[7,6,4,3,1]
```

13. Why is the answer `0` when prices continuously decrease?

14. Why do we maintain the minimum price so far?

15. Why can't we simply find the global minimum and maximum?

16. What is the brute-force complexity?

17. What is the optimal complexity?

18. Explain why the buy day must come before the sell day.

19. Dry-run:

```text
[3,8,1,5,7,2]
```

20. Dry-run:

```text
[2,4,1,10]
```

---

# 30. Final Mental Models

## Binary Exponentiation

```text
xⁿ
 ↓
Process binary bits of n
 ↓
Check n % 2
 ↓
If bit = 1 → ans *= x
 ↓
x *= x
 ↓
n /= 2
 ↓
Repeat
 ↓
O(log n)
```

Remember:

```text
Odd binary bit → multiply answer
Square x       → x *= x
Divide n       → n /= 2
```

## Best Time to Buy and Sell Stock

```text
Scan prices
    ↓
Track minimum price so far
    ↓
Treat current price as selling price
    ↓
profit = current - minimum
    ↓
Update maximum profit
    ↓
O(n)
```

Remember:

```text
bestBuy = minimum price so far

profit = current price - bestBuy

maxProfit = maximum profit so far
```

---

# ⭐ Final Takeaway

These two problems teach two powerful DSA patterns:

### Binary Exponentiation

```text
Repeated multiplication
        ↓
Binary representation
        ↓
Repeated squaring
        ↓
O(n) → O(log n)
```

### Best Time to Buy and Sell Stock

```text
Check every pair
        ↓
Track minimum buying price
        ↓
One-pass scan
        ↓
O(n²) → O(n)
```

The key is not merely memorizing the code.

Memorize the **invariant**:

> **Binary Exponentiation:** `ans` contains the product of the powers selected by the binary bits processed so far.

> **Stock:** `bestBuy` is the cheapest valid buying price seen so far, and `maxProfit` is the best valid profit found so far.
