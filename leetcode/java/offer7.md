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
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length == 0 || inorder.length == 0) {
            return null;
        }
        TreeNode root = new TreeNode(preorder[0]);

        int find = 0;
        for (int i = 0; i < inorder.length; i++) {
            if (inorder[i] == preorder[0]) {
                find = i;
                break;
            }
        }

        int[] leftinorder = new int[find];
        System.arraycopy(inorder, 0, leftinorder, 0, find);
        int[] rightinorder = new int[inorder.length - find - 1];
        System.arraycopy(inorder, find + 1, rightinorder, 0, inorder.length - find - 1);

        int[] leftpreorder = new int[find];
        System.arraycopy(preorder, 1, leftpreorder, 0, leftinorder.length);
        int[] rightpreorder = new int[preorder.length - find - 1];
        System.arraycopy(preorder, leftinorder.length + 1, rightpreorder, 0, preorder.length -  leftpreorder.length - 1);

        root.left = buildTree(leftpreorder, leftinorder);
        root.right = buildTree(rightpreorder, rightinorder);

        return root;
    }
}
```