```
给定一个可包含重复数字的序列 nums ，按任意顺序 返回所有不重复的全排列。

 

示例 1：

输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
示例 2：

输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
 

提示：

1 <= nums.length <= 8
-10 <= nums[i] <= 10
```

```

```

```
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        res = []

        def dfs(nums, trace, visited):
            if len(nums) == len(trace):
                res.append(trace[:])
                return
            
            for i in range(len(nums)):
                if visited[i]:
                    continue
                if i > 0 and nums[i] == nums[i - 1] and not visited[i - 1]:
                    continue
                trace.append(nums[i])
                visited[i] = True
                dfs(nums, trace, visited)
                trace.pop()
                visited[i] = False
        
        nums.sort()
        dfs(nums, [], [False for _ in range(len(nums))])
        return res
```