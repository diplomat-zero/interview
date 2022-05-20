```
输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

示例 1:
给定二叉树 [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7
返回 true 。

示例 2:
给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。

限制：
0 <= 树的结点个数 <= 10000
```

```

```

```
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($value) { $this->val = $value; }
 * }
 */
class Solution {

    /**
     * @param TreeNode $root
     * @return Boolean
     */
    function isBalanced($root) {
        if ($root == null) {
            return true;
        }
        $left = $this->height($root->left);
        $right = $this->height($root->right);
        if (abs($left - $right) > 1) {
            return false;
        }
        return $this->isBalanced($root->left) && $this->isBalanced($root->right);
    }

    function height($root) {
        if ($root == null) {
            return 0;
        }
        $left = $this->height($root->left);
        $right = $this->height($root->right);
        return $left > $right ? $left + 1 : $right + 1;
    }
}
```