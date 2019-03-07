The count-and-say sequence is the sequence of integers with the first five terms as following:

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

`1` is read off as `"one 1"` or `11`.
`11` is read off as `"two 1s"` or `21`.
`21` is read off as `"one 2`, then `one 1"` or `1211`.

Given an integer *n* where 1 ≤ *n* ≤ 30, generate the *n*th term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

 

**Example 1:**

```
Input: 1
Output: "1"
```

**Example 2:**

```
Input: 4
Output: "1211"
```



# Solution

```
class Solution(object):
    def countAndSay(self, n):
        s = '1'
        for _ in range(n - 1):
            s = re.sub(r'(.)\1*', lambda m:str(len(m.group(0))) + m.group(1), s)
        return s
```

re 是 regular expression 正則表達式  **[1]**

sub 為 substitute，表示替換

re.sub 透過正則表達式，實現比 replace 更強大的替換功能

舉例:

```inputStr = "hello 111 world 111"```

你可以用 replace這樣處理

``` replacedStr = inputStr.replace("111", "222")```

但是如果字串為

```inputStr = "hello 123 world 456"```

那麼就無法通過 replace 實現，而必須用正則表達式

```replacedStr = re.sub("\d+", "222", inputStr)```

---

其中第一個參數 ```r'(.)\1*'``` 之中 ```(.)\1``` 代表兩個連續的相同字元 **[2]** 而 ```*``` 代表符合前面的子運算式零次或多次。也就是說第一個參數將連續的字元區分成一組一組，例如 111221，111代表 $1，22代表$2，1代表$3。

第二個參數用 lambda 來分別處理第一個參數，lambda 是可以簡易來表達一個函數，舉例 **[3]**

```
def max(m, n):
	return m if m>n else n
```

``` max = lambda m, n: m if m>n else n ```

以上兩個都是表達同一個函數。

另外 group 為 re 的 功能，m.group(0) 的 m 如果是上面舉例 $1 的 111 那麼 group(0) 代表整個變數，group(1) 代表 111 裡面第一個 1，group(2) 代表 111 裡面第二個1...

---



### reference 

https://leetcode.com/problems/count-and-say/discuss/15999/4-5-lines-Python-solutions

**[1]** https://www.crifan.com/python_re_sub_detailed_introduction/

**[2]** https://zh.wikipedia.org/wiki/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F

**[3]** https://openhome.cc/Gossip/Python/LambdaExpression.html