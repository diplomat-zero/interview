```
给定一个整数数组  nums 和一个正整数 k，找出是否有可能把这个数组分成 k 个非空子集，其总和都相等。

 

示例 1：

输入： nums = [4, 3, 2, 3, 5, 2, 1], k = 4
输出： True
说明： 有可能将其分成 4 个子集（5），（1,4），（2,3），（2,3）等于总和。
示例 2:

输入: nums = [1,2,3,4], k = 3
输出: false
 

提示：

1 <= k <= len(nums) <= 16
0 < nums[i] < 10000
每个元素的频率在 [1,4] 范围内
```

```

```

```
func canPartitionKSubsets(nums []int, k int) bool {
    sum := 0
    for _,value := range nums {
        sum += value
    }
    if sum % k != 0 {
        return false
    }
    sort.Ints(nums)
    used := make(map[int]bool)
    find := sum / k
    var dfs func(int,int,int) bool
    dfs = func(index int, k int, sum int) bool {
        if k == 0 {
            return true
        }
        if sum == find {
            return dfs(0, k - 1, 0)
        }
        for i := index; i < len(nums); i++ {
            if used[i] {
                continue
            }
            if nums[i] > find {
                continue
            }
            if nums[i] + sum > find {
                continue
            }
            if (i > 0) && !used[i-1]  && nums[i] == nums[i-1] {
                continue
            }
            used[i] = true
            sum += nums[i]
            if (dfs(i + 1, k, sum)) {
                return true
            }
            used[i] = false
            sum -= nums[i]
        }
        return false
    }
    return dfs(0, k, 0) 
}
```