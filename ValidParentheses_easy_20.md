Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```
Input: "()"
Output: true
```

**Example 2:**

```
Input: "()[]{}"
Output: true
```

**Example 3:**

```
Input: "(]"
Output: false
```

**Example 4:**

```
Input: "([)]"
Output: false
```

**Example 5:**

```
Input: "{[]}"
Output: true
```



# Solution

```
class Solution(object):
    def isValid(self, s):
        if len(s) == 0:
            return True
        key = {')':'(', ']':'[', '}':'{'}
        queue_str = ''
        for i in s:
            if i == '(' or i == '[' or i =='{':
                queue_str += i
            else:
                if len(queue_str) == 0:
                    return False
                elif key[i] != queue_str[-1]:
                    return False
                else:
                    queue_str = queue_str[:-1]
        if len(queue_str) == 0:
               return True
        else:
               return False
```

* input 如果是空字串，則 return True
* 如果 input 是 '(', '[', '{' ，則存入 queue_str
* 如果 input 是 ')', ']', '}':
  * 之前必須要有 '(', '[', '{'，否則 return False
  * queue_str 最後的字串必須可以與這次 input 相符，否則 return False
  * queue_str 最後的字串與這次 input 相符，則刪除queue_str 最後的字串
* 最後檢查 queue_str 是否為空。