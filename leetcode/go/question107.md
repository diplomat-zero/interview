```
给你二叉树的根节点 root ，返回其节点值 自底向上的层序遍历 。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

 

示例 1：


输入：root = [3,9,20,null,null,15,7]
输出：[[15,7],[9,20],[3]]
示例 2：

输入：root = [1]
输出：[[1]]
示例 3：

输入：root = []
输出：[]
 

提示：

树中节点数目在范围 [0, 2000] 内
-1000 <= Node.val <= 1000
```

```

```

```
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func levelOrderBottom(root *TreeNode) [][]int {
    res := make([][]int, 0)
    if root == nil {
        return res
    }
    stack := make([]*TreeNode, 0)
    stack = append(stack, root)

    for len(stack) > 0 {
        length := len(stack)
        tmp := make([]int, 0)
        for i := 0; i < length; i++ {
            node := stack[0]
            stack = stack[1:]
            tmp = append(tmp, node.Val)
            if node.Left != nil {
                stack = append(stack, node.Left)
            }
            if node.Right != nil {
                stack = append(stack, node.Right)
            }
        }
        res = append(res, tmp)
    }
    left := 0
    right := len(res) - 1
    for left < right {
        res[left], res[right] = res[right], res[left]
        left++
        right--
    }
    return res
}
```