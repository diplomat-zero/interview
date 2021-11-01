```
从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回：
[3,9,20,15,7]
 
提示：
节点总数 <= 1000
```

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[int]:
        ret = []
        if root is None:
            return ret

        queue = []

        queue.append(root)

        while (len(queue) > 0):
            node = queue[0]
            queue.remove(queue[0])
            ret.append(node.val)
            if (node.left is not None):
                queue.append(node.left)
            if (node.right is not None):
                queue.append(node.right)

        return ret
```