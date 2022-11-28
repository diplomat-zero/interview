```
给定一个非负整数数组 nums ，你最初位于数组的 第一个下标 。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个下标。

 

示例 1：

输入：nums = [2,3,1,1,4]
输出：true
解释：可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。
示例 2：

输入：nums = [3,2,1,0,4]
输出：false
解释：无论怎样，总会到达下标为 3 的位置。但该下标的最大跳跃长度是 0 ， 所以永远不可能到达最后一个下标。
 

提示：

1 <= nums.length <= 3 * 104
0 <= nums[i] <= 105
```

```

```

```
func canJump(nums []int) bool {
    //前n-1个元素能够跳到的最远距离
    far := 0 
    for i := 0; i <= far; i++ {
        //第i个元素能够跳到的最远距离
        i_far := i + nums[i]   
        far = max(far, i_far)
        if far >= len(nums) - 1 {
            // 如果最远距离已经大于或等于最后一个元素的下标,则说明能跳过去,退出. 减少循环
            return true
        }
    }
    //最远距离k不再改变,且没有到末尾元素
    return false
}

func max(a,b int) int {
    if a > b {
        return a
    }
    return b
}
```

```
func canJump(nums []int) bool {
    far := 0
    for i := 0; i < len(nums) - 1; i++ {
        if i + nums[i] > far {
            far = i + nums[i]
        }
        if far <= i {
            return false
        }
    }
    return far >= len(nums) - 1
}
```