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
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        return self.isSame(root.left, root.right)


    def isSame(self, leftNode: TreeNode, rightNode: TreeNode) -> bool:
        if leftNode is None and rightNode is None:
            return True
        if leftNode is None or rightNode is None:
            return False
        
        return leftNode.val == rightNode.val and self.isSame(leftNode.left, rightNode.right) and self.isSame(leftNode.right, rightNode.left)
```