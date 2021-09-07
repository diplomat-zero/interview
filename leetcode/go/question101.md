```
给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    1
   / \
  2   2
 / \ / \
3  4 4  3
 
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3
 

进阶：
你可以运用递归和迭代两种方法解决这个问题吗？
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
func isSymmetric(root *TreeNode) bool {
    return isSame(root.Left, root.Right)
}

func isSame(leftNode *TreeNode, rightNode *TreeNode) bool {
    if (leftNode == nil && rightNode == nil) {
        return true;
    }
    if (leftNode == nil || rightNode == nil) {
        return false;
    }

    return leftNode.Val == rightNode.Val && isSame(leftNode.Left, rightNode.Right) && isSame(leftNode.Right, rightNode.Left)
}
```