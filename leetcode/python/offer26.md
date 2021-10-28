```
输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)
B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

     3
    / \
   4   5
  / \
 1   2
给定的树 B：

   4 
  /
 1
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

示例 1：
输入：A = [1,2,3], B = [3,1]
输出：false

示例 2：
输入：A = [3,4,5,1,2], B = [4,1]
输出：true

限制：
0 <= 节点个数 <= 10000
```

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSubStructure(self, A: TreeNode, B: TreeNode) -> bool:
        if A is None or B is None:
            return False
        if A is None and B is None:
            return True

        return self.isSub(A, B) or self.isSubStructure(A.left, B) or self.isSubStructure(A.right, B)


    def isSub(self, A: TreeNode, B: TreeNode) -> bool:
        if B is None:
            return True

        if A is None:
            return False

        if A.val == B.val:
            return self.isSub(A.left, B.left) and self.isSub(A.right, B.right)

        return False
```