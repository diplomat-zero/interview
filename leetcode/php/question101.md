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
<?php
class TreeNode {
    public $val = null;

    public $left = null;

    public $right = null;

    function __construct($val = 0, $left = null, $right = null) {
        $this->val = $val;
        $this->left = $left;
        $this->right = $right;
    }
}
class Solution {
    /**
     * @param TreeNode $root
     *
     * @return Boolean
     */
    function isSymmetric($root) {
        return $this->isSame($root->left, $root->right);
    }

    function isSame($left, $right) {
        if ($left == null && $right == null) {
            return true;
        }
        if ($left == null || $right == null) {
            return false;
        }

        return $left->val == $right->val && $this->isSame($left->left, $right->right) && $this->isSame($left->right, $right->left);
    }
}
```