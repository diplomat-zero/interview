```
给定一个二叉树，判断它是否是高度平衡的二叉树。
本题中，一棵高度平衡二叉树定义为：
一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1 。

示例 1：
输入：root = [3,9,20,null,null,15,7]
输出：true

示例 2：
输入：root = [1,2,2,3,3,null,null,4,4]
输出：false

示例 3：
输入：root = []
输出：true
 
提示：
树中的节点数在范围 [0, 5000] 内
-104 <= Node.val <= 104
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
     * @return Boolean
     */
    function isBalanced($root) {
        if ($root == null) {
            return true;
        }
        $left_height = self::height($root->left);
        $right_height = self::height($root->right);
        if (abs($left_height - $right_height) > 1) {
            return false;
        }

        if (!self::isBalanced($root->left)) {
            return false;
        }
        if (!self::isBalanced($root->right)) {
            return false;
        }

        return true;
    }

    function height($tree) {
        if ($tree == null) {
            return 0;
        }
        $left = self::height($tree->left);
        $right = self::height($tree->right);
        return $left > $right ? $left + 1 : $right + 1;
    }
}
```