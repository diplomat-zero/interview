```
计算给定二叉树的所有左叶子之和。

示例：

    3
   / \
  9  20
    /  \
   15   7

在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24
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
     * @return Integer
     */
    function sumOfLeftLeaves($root) {
        $result = 0;
        self::sum($root, $result);
        return $result;
    }

    function sum($root, &$result) {
        if ($root == null) {
            return;
        }
        if ($root->left != null && $root->left->left == null && $root->left->right == null) {
            $result += $root->left->val;
        }
        self::sum($root->left, $result);
        self::sum($root->right, $result);
    }
}
```