You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```



# Solution

Suppose d[i] = max money for up to _i_ th home

Therefore, d[i] = max( d[i-1], d[i-2]+nums[i] )

## Recursion

```
class Solution(object):

    def dp(self, nums, i, res):
        if i < 0:
            return 0
        if res[i] >= 0:
            return res[i]
        else:
            res[i] = max(self.dp(nums, i - 1, res), self.dp(nums, i - 2, res) + nums[i])
        return res[i]

    def rob(self, nums):
        n = len(nums)
        res = [-1]*n
        return self.dp(nums, n - 1, res)
```



## Dynamic Programming



```
class Solution(object):
    def rob(self, nums):
        if len(nums) == 0:
            return 0
        elif len(nums) ==1 :
            return nums[0]
        money = [0]*len(nums)
        money[0], money[1] = nums[0], max(nums[0], nums[1])
        for i in xrange(2, len(nums)):
            money[i] = max(nums[i] + money[i-2], money[i-1])
        return money[len(nums)-1]
```



## Dynamic Programming (optimization)

上面的代碼使用的空間是冗餘的，因為每次循環只會用到前兩個數據。所以代碼可以降低空間複雜度到O(1)。

```
class Solution(object):
    def rob(self, nums):
        now = last = 0
        for i in nums:
            last, now = now, max(i+last, now)
        return now
```



### reference

https://blog.csdn.net/coder_orz/article/details/51555813

http://songhuiming.github.io/pages/2018/03/18/leetcode-198-house-robber/

https://leetcode.com/problems/house-robber/discuss/156523/From-good-to-great.-How-to-approach-most-of-DP-problems.