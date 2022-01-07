```
给你一个由 n 个整数组成的数组 nums ，和一个目标值 target 。请你找出并返回满足下述全部条件且不重复的四元组 [nums[a], nums[b], nums[c], nums[d]] （若两个四元组元素一一对应，则认为两个四元组重复）：
0 <= a, b, c, d < n
a、b、c 和 d 互不相同
nums[a] + nums[b] + nums[c] + nums[d] == target
你可以按 任意顺序 返回答案 。

示例 1：
输入：nums = [1,0,-1,0,-2,2], target = 0
输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]

示例 2：
输入：nums = [2,2,2,2,2], target = 8
输出：[[2,2,2,2]]
 
提示：
1 <= nums.length <= 200
-109 <= nums[i] <= 109
-109 <= target <= 109
```

```
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums = sorted(nums)
        result = []
        length = len(nums)
        for i in range(len(nums)):
            m = i + 1
            for j in range(m, len(nums)):
                find = target - nums[i] - nums[j]
                left = j + 1
                right = len(nums) - 1
                while left < right:
                    tmp = []
                    if nums[left] + nums[right] == find:
                        tmp.append(nums[i])
                        tmp.append(nums[j])
                        tmp.append(nums[left])
                        tmp.append(nums[right])
                        tmp = sorted(tmp)
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