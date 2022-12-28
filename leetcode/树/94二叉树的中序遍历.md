```
给定一个二叉树的根节点 root ，返回它的 中序 遍历。

示例 1：
输入：root = [1,null,2,3]
输出：[1,3,2]

示例 2：
输入：root = []
输出：[]

示例 3：
输入：root = [1]
输出：[1]

示例 4：
输入：root = [1,2]
输出：[2,1]

示例 5：
输入：root = [1,null,2]
输出：[1,2]
 
提示：

树中节点数目在范围 [0, 100] 内
-100 <= Node.val <= 100
 
进阶: 递归算法很简单，你可以通过迭代算法完成吗
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
func inorderTraversal(root *TreeNode) []int {
    res = make([]int, 0)
    inorder(root)
    return res
}

func inorder(root *TreeNode)  {
    if (root == nil) {
        return
    }
    inorder(root.Left)
    res = append(res, root.Val)
    inorder(root.Right)
}
```