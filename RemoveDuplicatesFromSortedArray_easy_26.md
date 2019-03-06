Given a sorted array *nums*, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only *once* and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

**Example 1:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

特別注意，雖然 return 是一個正整數，但是同時系統也會檢查 input 的 nums 是否有被你移除重複的 element，系統只在意 return 正整數長度之內 nums 的 element。

# Solution

## failed case

```
class Solution(object):
    def removeDuplicates(self, nums):
        if len(nums) == 0:
            return 0
        init = nums[0]
        res = 1
        for i in nums[1:]:
            if i != init:
                init = i
                res += 1
        return res
```

原因: 雖然 return 的長度是對的，但是沒有移除重複的 element。

Input:[1,1,2]

Output:[1,1]

Expected:[1,2]



## success case

```
class Solution(object):
    def removeDuplicates(self, nums):
        if len(nums) == 0:
            return 0
        init = nums[0]
        res = 1
        for i in nums[1:]:
            if i != init:
                nums[res] = i
                init = nums[res]
                res += 1
        return res
```

