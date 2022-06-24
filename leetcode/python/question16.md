```
给你一个长度为 n 的整数数组 nums 和 一个目标值 target。请你从 nums 中选出三个整数，使它们的和与 target 最接近。

返回这三个数的和。

假定每组输入只存在恰好一个解。

 

示例 1：

输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
示例 2：

输入：nums = [0,0,0], target = 1
输出：0
 

提示：

3 <= nums.length <= 1000
-1000 <= nums[i] <= 1000
-104 <= target <= 104
```

```

```

```
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        num_sum = nums[0] + nums[1] + nums[len(nums) - 1]
        for i in range(len(nums)):
            left = i + 1
            right = len(nums) - 1
            while left < right:
                sum_num = nums[i] + nums[left] + nums[right]
                if abs(sum_num - target) < abs(num_sum - target):
                    num_sum = sum_num
                
                if sum_num > target:
                    right -= 1
                elif sum_num < target:
                    left += 1
                else:
                    return sum_num
        
        return num_sum
```