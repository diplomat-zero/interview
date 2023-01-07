```
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。

 

参考以下这颗二叉搜索树：

     5
    / \
   2   6
  / \
 1   3
示例 1：

输入: [1,6,3,2,5]
输出: false
示例 2：

输入: [1,3,2,6,5]
输出: true
 

提示：

数组长度 <= 1000
```

```

```

```
func verifyPostorder(postorder []int) bool {
    var helper func([]int, int, int) bool
    helper = func(postorder[]int, left int, right int) bool {
        if left >= right {
            return true
        }
        start := left
        for start < right && postorder[start] < postorder[right] {
            start++
        }
        end := start
        for end < right && postorder[end] > postorder[right] {
            end++
        }
        return end == right && helper(postorder, left, start - 1) && helper(postorder, start, right - 1)
    }
    return helper(postorder, 0, len(postorder) - 1)
}
```