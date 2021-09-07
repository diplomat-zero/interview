```
给定一个二叉树，判断它是否是高度平衡的二叉树。
本题中，一棵高度平衡二叉树定义为：
一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1 。

示例 1：
输入：root = [3,9,20,null,null,15,7]
输出：true

示例 2：
输入：root = [1,2,2,3,3,null,null,4,4]
输出：false

示例 3：
输入：root = []
输出：true
 
提示：
树中的节点数在范围 [0, 5000] 内
-104 <= Node.val <= 104
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
func isBalanced(root *TreeNode) bool {
    if (root == nil) {
        return true
    }
    if (int(math.Abs(height(root.Left) - height(root.Right))) > 1) {
        return false
    }

    if (!isBalanced(root.Left)) {
        return false
    }
    if (!isBalanced(root.Right)) {
        return false
    }

    return true
}

func height(root * TreeNode) float64 {
    if (root == nil) {
        return 0
    }
    left_height := height(root.Left)
    right_height := height(root.Right)
    if (left_height > right_height) {
        return left_height + 1
    } else {
        return right_height + 1
    }
}
```