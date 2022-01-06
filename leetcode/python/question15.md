```
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。
注意：答案中不可以包含重复的三元组。

示例 1：
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]

示例 2：
输入：nums = []
输出：[]

示例 3：
输入：nums = [0]
输出：[]
 
提示：
0 <= nums.length <= 3000
-105 <= nums[i] <= 105
```

```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums = sorted(nums)
        right = len(nums) - 1
        result = []
        length = len(nums)
        for i, num in enumerate(nums):
            find = 0 - num
            left = i + 1
            right = len(nums) - 1
            while left < right:
                tmp = []
                if nums[left] + nums[right] == find:
                    tmp.append(num)
                    tmp.append(nums[left])
                    tmp.append(nums[right])
                    if tmp not in result:
                        result.append(tmp)
                    tmp_left = left + 1
                    while tmp_left < length and nums[tmp_left] == nums[left]:
                        tmp_left += 1
                    left = tmp_left
                    tmp_right = right - 1
                    while tmp_right > 0 and nums[tmp_right] == nums[right]:
                        tmp_right -= 1
                    right = tmp_right
                elif nums[left] + nums[right] < find:
                    left += 1
                else:
                    right -= 1
        
        return result
```