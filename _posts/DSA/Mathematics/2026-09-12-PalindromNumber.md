---
title: "Is Number Palindrome?"
topic: DSA > Mathematics
summary: "Is a given number Palindrome?"
---

Task: To check if a number is palindrome. 

I/P: Let's say we have been given an input of n where n is a number and is greater than 0. 

Expected O/P: If the reverse of the number is same as the number, then return True(Palindrome) else False(Not a palindrome).
Example: 

| X | Palindrome?|
|---|---|
| 8668 | True |
| 38 | False |
| 8 | True |

Notes: It is easier to find the reverse of a number by using the logic x=x%10 = which gives the remainder of the number.


```python
def isDigitPalindrome(n):
  #calculate the reverse of a number.
  rev= 0
  #Create a temp variable to store the n value so that it does not get modified for comparison later.
  temp=n
  while temp > 0:
    # Divide temp by 10 until it is 0.
    last_digit= temp %10
    rev= rev * 10 + last_digit 
    temp = temp // 10

  return (rev==n) 
```

**Time Complexity:** O(n) 
