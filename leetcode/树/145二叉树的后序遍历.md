```
给定一个二叉树，返回它的 后序 遍历。

示例:
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 
输出: [3,2,1]
进阶: 递归算法很简单，你可以通过迭代算法完成吗？
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
var res []int
func postorderTraversal(root *TreeNode) []int {
    res = make([]int, 0)
    postorder(root)
    return res
}

func postorder(root *TreeNode) {
    if root == nil {
        return
    }
    postorder(root.Left)
    postorder(root.Right)
    res = append(res, root.Val)
}
```