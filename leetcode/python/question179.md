```
给定一组非负整数 nums，重新排列每个数的顺序（每个数不可拆分）使之组成一个最大的整数。

注意：输出结果可能非常大，所以你需要返回一个字符串而不是整数。

 

示例 1：

输入：nums = [10,2]
输出："210"
示例 2：

输入：nums = [3,30,34,5,9]
输出："9534330"
 

提示：

1 <= nums.length <= 100
0 <= nums[i] <= 109
```

```

```

```
class Solution:
    def largestNumber(self, nums: List[int]) -> str:
        res = ''
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                str1 = str(nums[i])
                str2 = str(nums[j])
                if str1 + str2 < str2 + str1:
                    nums[i], nums[j] = nums[j], nums[i]
        
        for j in range(len(nums)):
            if j == 0 and nums[j] == 0:
                return '0'
            res = res + str(nums[j])
        
        return res
```