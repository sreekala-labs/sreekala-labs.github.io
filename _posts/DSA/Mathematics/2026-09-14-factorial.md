---
title: "Factorial of a number"
topic: DSA > Mathematics
summary: "Compute the factorial of a number, assuming n>=0 -> Iterative and Recrusive Solution."
---

Factorial of a number is written as n!, calculated by mutiplying the number down to 1. 
Example: 5!= 5*4*3*2*1 = 120 
Special Rule is : 0!= 1

Where can you use Factorial: 
* Permutations: Finding how many ways you can arrange items, like lining up 5 people in a row (\(5! = 120\) ways).
* Combinations: Calculating group selections where order does not matter.
* Probability: Working out the odds of specific events, like card hands or lottery numbers.
* Calculus and Analysis: Power series expansions for functions like \(e^{x}\) (the exponential function).
* Computer Science: Used as a basic example to teach recursion and loops in programming languages.

There are two ways factorial of a number can be implemented. Iterative and Recrusive. 

**Iterative Solution:**

```python
def factorial(n):
  result = 1
  for i in range(2, n+1):
    result = result * i

  return result 
```
Space Complexity: Since we using only variables which are of type int, the space complexity here is O(1).

Time Complexity: O(n) since we have to iterative n times. n being the number. 


**Factorial Solution:**
```python
def factorial(n):
  #Exit Condition
  if n==0:
    return 1
  #Logic
  return n * factorial(n-1)
```
Space Complexity: Since we are using Recursion, the calls are stored in a stack.(Extra Overhead). So Space Complexity is O(n).

Time  Complexity: This has to compute by reduce n to n-1 until n becomes 1, O(n) is the time complexity.

An iterative solution is better because it avoids the risk of stack overflow errors and uses less memory by storing 
calculations in a single loop rather than creating a new memory layer for every recursive call.
