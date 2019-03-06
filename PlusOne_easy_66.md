Given a **non-empty** array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

把一個 input 的 list 想像成一個正整數，output 為這正整數加一的 list

**Example 1:**

```
Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

**Example 2:**

```
Input: [9,9,9,9]
Output: [1,0,0,0,0]
Explanation: The array represents the integer 9999.
```

**Example 3:**

```
Input: [5,0,3,9]
Output: [5,0,4,0]
Explanation: The array represents the integer 5039.
```



# Solution

```
class Solution(object):
    def plusOne(self, digits):
        for i in range(len(digits)-1, -1, -1):
            x = digits[i] +1
            if x < 10:
                digits[i] = x
                return digits
            else:
                digits[i] = 0
        if digits[0] == 0:
            digits.insert(0, 1)
        return digits
```



