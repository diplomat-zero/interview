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
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length == 0) {
            return null;
        }
        int root_val = preorder[0];
        TreeNode root = new TreeNode(root_val);
        int find = 0;
        for (int i = 0; i < inorder.length; i++) {
            if (inorder[i] == root_val) {
                find = i;
                break;
            }
        }

        int[] left_preorder = Arrays.copyOfRange(preorder, 1, find + 1);
        int[] right_preorder = Arrays.copyOfRange(preorder, find + 1, preorder.length);
        int[] left_inorder = Arrays.copyOfRange(inorder, 0, find);
        int[] right_inorder = Arrays.copyOfRange(inorder, find + 1, inorder.length);

        root.left = buildTree(left_preorder, left_inorder);
        root.right = buildTree(right_preorder, right_inorder);
        return root;
    }
}
```