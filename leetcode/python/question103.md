```
给你二叉树的根节点 root ，返回其节点值的 锯齿形层序遍历 。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

示例 1：
输入：root = [3,9,20,null,null,15,7]
输出：[[3],[20,9],[15,7]]

示例 2：
输入：root = [1]
输出：[[1]]

示例 3：
输入：root = []
输出：[]
 
提示：
树中节点数目在范围 [0, 2000] 内
-100 <= Node.val <= 100
```

```

```

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        if root is None:
            return []
        result = []
        stack = []
        stack.append(root)
        while len(stack) > 0:
            length = len(stack)
            tmp = []
            for i in range(length):
                node = stack.pop(0)
                tmp.append(node.val)
                if node.left:
                    stack.append(node.left)
                if node.right:
                    stack.append(node.right)
            result.append(tmp)
        
        ret = []
        for i in range(len(result)):
            if i % 2 == 0:
                ret.append(result[i])
            else:
                tmp = list(reversed(result[i]))
                ret.append(tmp)

        return ret                
```