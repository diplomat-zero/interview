```
给你一个整数数组 nums，请你将该数组升序排列。

 

示例 1：

输入：nums = [5,2,3,1]
输出：[1,2,3,5]
示例 2：

输入：nums = [5,1,1,2,0,0]
输出：[0,0,1,1,2,5]
 

提示：

1 <= nums.length <= 5 * 104
-5 * 104 <= nums[i] <= 5 * 104
```

```

```

```
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        self.quickSort(nums, 0, len(nums) - 1)
        return nums

    
    def quickSort(self, nums, start, end):
        if start < end:
            find = self.findNum(nums, start, end)
            self.quickSort(nums, start, find - 1)
            self.quickSort(nums, find + 1, end)


    def findNum(self, nums, start, end):
        target = nums[start]
        while start < end :
            while start < end and target <= nums[end]:
                end -= 1
            nums[start],nums[end] = nums[end], nums[start]
            while start < end and target >= nums[start]:
                start += 1
            nums[start],nums[end] = nums[end], nums[start]
        return start
```