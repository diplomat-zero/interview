```
给你一个整数数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回 滑动窗口中的最大值 。

 

示例 1：

输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
示例 2：

输入：nums = [1], k = 1
输出：[1]
 

提示：

1 <= nums.length <= 105
-104 <= nums[i] <= 104
1 <= k <= nums.length
```

```

```

```
func maxSlidingWindow(nums []int, k int) []int {
    res := make([]int, 0)
    windows := initDequeue()
    for i := 0; i < len(nums); i++ {
        if i < k - 1 {
            windows.push(nums[i])
        } else {
            windows.push(nums[i])
            res = append(res, windows.max())
            windows.pop(nums[i - k + 1])
        }
    }
    return res
}

type dequeue struct {
    queue []int
}

func initDequeue() *dequeue {
    return &dequeue{[]int{}}
}

func (this *dequeue) push(x int) {
    for len(this.queue) > 0 && this.queue[len(this.queue) - 1] < x {
        this.queue = this.queue[:len(this.queue) - 1]
    } 
    this.queue = append(this.queue, x)
}

func (this *dequeue) pop(x int) {
    if len(this.queue) > 0 && this.queue[0] == x {
        this.queue = this.queue[1:]
    }
}

func (this *dequeue) max() int {
    return this.queue[0]
}
```