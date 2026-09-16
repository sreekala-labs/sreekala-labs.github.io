---
title: "Trailing Zeroes in Factorial of a number"
topic: DSA > Mathematics
summary: "Compute the Trailing Zeroes in factorial of a number"
---

Trailing Zeroes are the number of zeroes which appear at the end of the resulting number. 

Example: 5!=5*4*3*2*1 = 120 - Trailing Zero is 1 

10! = 10*9*8*7*6*5*4*3*2*1 = 3628800 = Trailing Zeros -> 2 

**Naive Solution:**

First thing that comes to mind is that you can calculate the factorial and then start dividing and performing modulus operation by 10 
to get the reminder

```python
def trailingZeroes(n):
  fact = 1
  for i in range(2,n+1):
        fact = fact * i

  count=0
  while fact % 10 ==0:
    count+=1
    fact = fact // 10

  return fact
```

Space Complexity:  This loop divides the massive factorial by 10 repeatedly. Each modulo (%) and integer division (//) operation 
on a giant number takes time proportional to the number of digits. 
Since there are roughly \(n/5\) trailing zeros, this loop also scales to \(O(n^2)\).

Time  Complexity: O(n^2)


**Better and optimal way:**
To find the number of trailing zeros, for example 251!, you don't need to calculate the full number. 
Instead, you count how many times the factor 5 appears in the numbers from 1 to 251 
(since every pair of 2 and 5 creates a trailing zero, and there are always plenty of 2s).
You can find this quickly using **Legendre's Formula** by dividing 251 by powers of 5 and 
discarding the remainders:

251 ÷ 5 = 50 (with a remainder of 1) → 50

251 ÷ 25 = 10 (with a remainder of 1) → 10 

251 ÷ 125 = 2 (with a remainder of 1) → 2

Now, add these quotients together:\(50+10+2=62\)

```python
def trailingZeros(n):
  res = 0
  i = 5
  while i <=n:
    res = res + n//i
    i = i*5
  return res 
```

Time Complexity: Since we are multiplying or incrementing the i value by 5, the time complexity is O($\log_5(x)$)

Space Complexity: O(1) since only integer types are being used. 

