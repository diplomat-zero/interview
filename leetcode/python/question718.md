```
给两个整数数组 nums1 和 nums2 ，返回 两个数组中 公共的 、长度最长的子数组的长度 。

 

示例 1：

输入：nums1 = [1,2,3,2,1], nums2 = [3,2,1,4,7]
输出：3
解释：长度最长的公共子数组是 [3,2,1] 。
示例 2：

输入：nums1 = [0,0,0,0,0], nums2 = [0,0,0,0,0]
输出：5
 

提示：

1 <= nums1.length, nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 100
```

```

```

```
class Solution:
    def findLength(self, nums1: List[int], nums2: List[int]) -> int:
        len1 = len(nums1)
        len2 = len(nums2)
        max_len = 0

        dp = [[0] * (len2 + 1) for _ in range(len1 + 1)]

        for i in range(1, len1 + 1):
            for j in range(1, len2 + 1):
                if nums1[i - 1] == nums2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + 1
                else:
                    dp[i][j] = 0
                max_len = max(max_len, dp[i][j])
        
        return max_len
```