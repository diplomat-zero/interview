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
    public boolean isSymmetric(TreeNode root) {
        return isSame(root, root);
    }

    public boolean isSame(TreeNode l, TreeNode r) {
        if (l == null && r == null) {
            return true;
        } 
        if (l == null || r == null) {
            return false;
        }

        return l.val == r.val && isSame(l.left, r.right) && isSame(l.right, r.left);
    }
}
```