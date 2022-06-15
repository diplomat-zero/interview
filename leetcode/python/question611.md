```
给定一个包含非负整数的数组 nums ，返回其中可以组成三角形三条边的三元组个数。

示例 1:
输入: nums = [2,2,3,4]
输出: 3
解释:有效的组合是: 
2,3,4 (使用第一个 2)
2,3,4 (使用第二个 2)
2,2,3

示例 2:
输入: nums = [4,2,3,4]
输出: 4
 
提示:
1 <= nums.length <= 1000
0 <= nums[i] <= 1000
```

```

```

```
class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        nums.sort()

        res = 0
        p = len(nums) - 1
        while p >= 2:
            l = 0
            r = p - 1
            while l < r:
                if nums[l] + nums[r] > nums[p]:
                    res += r - l
                    r -= 1
                else:
                    l += 1
            p -= 1
        
        return res
```