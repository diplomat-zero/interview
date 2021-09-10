```
给定一个二叉树，返回所有从根节点到叶子节点的路径。
说明: 叶子节点是指没有子节点的节点。

示例:
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]
解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        result = []
        trace = {}
        trace[root] = 1
        self.dfs(root, result, trace)
        return result


    def dfs(self, root, result, trace) -> None:
        if root.left is None and root.right is None:
            tmp = ""
            for value in trace:
                tmp += str(value.val)
                tmp += '->'
            tmp = tmp[:-2]
            result.append(tmp)

        if root.left:
            if root.left not in trace:
                trace[root.left] = 1
                self.dfs(root.left, result, trace)
                del trace[root.left]

        if root.right:
            if root.right not in trace:
                trace[root.right] = 1
                self.dfs(root.right, result, trace)
                del trace[root.right]
```