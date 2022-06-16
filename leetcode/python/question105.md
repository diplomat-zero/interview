```
给定两个整数数组 preorder 和 inorder ，其中 preorder 是二叉树的先序遍历， inorder 是同一棵树的中序遍历，请构造二叉树并返回其根节点。

示例 1:
输入: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
输出: [3,9,20,null,null,15,7]

示例 2:
输入: preorder = [-1], inorder = [-1]
输出: [-1]
 
提示:
1 <= preorder.length <= 3000
inorder.length == preorder.length
-3000 <= preorder[i], inorder[i] <= 3000
preorder 和 inorder 均 无重复 元素
inorder 均出现在 preorder
preorder 保证 为二叉树的前序遍历序列
inorder 保证 为二叉树的中序遍历序列
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
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if len(preorder) == 0:
            return None
        root_val = preorder[0]
        root = TreeNode(root_val)

        find = 0
        for i in range(len(inorder)):
            if inorder[i] == root_val:
                find = i
                break
        
        left_preorder = preorder[1:1 + find]
        right_preorder = preorder[1 + find:len(preorder)]
        
        left_inorder = inorder[0:find]
        right_inorder = inorder[find + 1:len(inorder)]

        left = self.buildTree(left_preorder, left_inorder)
        right = self.buildTree(right_preorder, right_inorder)

        root.left = left
        root.right = right
        return root
```