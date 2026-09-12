---
title: "Count the number of Digits"
topic: Mathematics
summary: "Count the number of Digits of give number"
---

Task: Count the number of digits of a given number. 

I/P: Let's say we have been given an input of X where X is a number and is greater than 0. 

Expected O/P: Number of digits of the given number. 
Example: 

| X | Digits|
|---|---|
| 9235 | 4 |
| 38 | 2 |
| 7 | 1 |

```python
def countOfDigits(X):
  # Declare a constant count which will be returned.
  count = 0
  while X > 0:
    # Divide X by 10 until it is 0. 
    X = X // 10
    count +=1
  return count 
```

| X | Logic | Count |
|---|---|---|
| 9235  | 9235/10 = 923 | Count = 1 |
| 923  | 923/10 = 92 | Count = 2 |
| 92  | 92/10 = 9 | Count = 3 |
| 9  | 9/10 = 0 | Count = 4 |
