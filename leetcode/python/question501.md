```
给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

结点左子树中所含结点的值小于等于当前结点的值
结点右子树中所含结点的值大于等于当前结点的值
左子树和右子树都是二叉搜索树
例如：
给定 BST [1,null,2,2],

   1
    \
     2
    /
   2
返回[2].

提示：如果众数超过1个，不需考虑输出顺序

进阶：你可以不使用额外的空间吗？（假设由递归产生的隐式调用栈的开销不被计算在内）
```

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findMode(self, root: TreeNode) -> List[int]:
        ret = {}
        self.inorder(root, ret)
        res = []
        for k, v in ret.items():
            if len(res) is 0:
                res.append(k)
                max = v
            else:
                if v > max:
                    max = v
                    res.clear()
                    res.append(k)
                elif v == max:
                    res.append(k)

        return res

    def inorder(self, root: TreeNode, ret) -> None:
        if not root:
            return;

        self.inorder(root.left, ret)
        if ret.get(root.val):
            ret[root.val] = ret.get(root.val) + 1
        else:
            ret[root.val] = 1            
        self.inorder(root.right, ret)
```