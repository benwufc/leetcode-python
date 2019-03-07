Given an integer *n*, return the number of trailing zeroes in *n*!.

**Example 1:**

```
Input: 3
Output: 0
Explanation: 3! = 6, no trailing zero.
```

**Example 2:**

```
Input: 5
Output: 1
Explanation: 5! = 120, one trailing zero.
```

**Note:** Your solution should be in logarithmic time complexity.



# Solution

## Time Limit Exceeded

```
class Solution(object):
    def factorial(self, n):
        if n == 0:
            return 1
        num = 1
        while n > 0:
            num = num*n
            n -= 1
        return num
    def trailingZeroes(self, n):
        n_fac = self.factorial(n)
        res = 0
        while n_fac % 10 == 0:
            res +=1
            n_fac = n_fac // 10
        return res
```

因為複雜度 O( _2n_ ) > O( log _n_ )



## success 

試想如果尾數要有 0，勢必其因數為 2, 5 所構成，又因為因數 2 的數量遠高於 因數 5，因此我們只需要關心 n! 會有多少因數 5。

### iteration

```
class Solution(object):
    def trailingZeroes(self, n):
        res = 0
        while n > 0:
            n = n/5
            res += n
        return res
```

### recursion

```
class Solution(object):
    def trailingZeroes(self, n):
		return 0 if n == 0 else n / 5 + self.trailingZeroes(n / 5)
```

**n/5** 這概念是想， $n! = n \times (n-1) \times \dots \times 2 \times 1$  這 $n$ 個數字，每五次會有一次有因數 5，但是如果因數是 25的話，則會有兩個 5，這種情況是**每五次會有一次有因數 5 之中每五次會發生一次** ，同理 125會有三個5，依此類推。

舉例: $135!$ : 135/5 = 27，有 27 個因數5，而這 27個之中，每五個會有一次因數25，因此 27/5=5，而這 5 個之中，每五個會有一次因數 125，因此 5/5=1。所以 $135! $ 會有 27+5+1=33，33個因數 5，有 33 個尾數 0。

**Note:** python 當中 m/n = x ， output 值 x 為商!

















