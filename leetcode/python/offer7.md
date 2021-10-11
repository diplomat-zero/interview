```
输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。
假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

示例 1:
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]

示例 2:
Input: preorder = [-1], inorder = [-1]
Output: [-1]
 
限制：
0 <= 节点个数 <= 5000
```

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if len(preorder) == 0 or len(inorder) == 0 :
            return None

        find = 0
        for i in range(len(inorder)):
            if inorder[i] == preorder[0]:
                find = i
                break
        
        leftinorder = inorder[0:find]
        rightinorder = inorder[find + 1:]
        
        leftpreorder = preorder[1:len(leftinorder) + 1]
        rightpreorder = preorder[len(leftinorder) + 1:]

        root = TreeNode(preorder[0])
        root.left = self.buildTree(leftpreorder, leftinorder)
        root.right = self.buildTree(rightpreorder, rightinorder)

        return root
```