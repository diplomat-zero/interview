```
翻转一棵二叉树。

示例：
输入：
     4
   /   \
  2     7
 / \   / \
1   3 6   9
输出：

     4
   /   \
  7     2
 / \   / \
9   6 3   1
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
     * @return TreeNode
     */
    function invertTree($root) {
        if ($root == null) {
            return;
        }
        $tmp = $root->left;
        $root->left = $root->right;
        $root->right = $tmp;
        self::invertTree($root->left);
        self::invertTree($root->right);
        return $root;
    }
}
```

```
这个比上面的更快
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
     * @return TreeNode
     */
    function invertTree($root) {
        if ($root == null) {
            return;
        }
        self::invertTree($root->left);
        self::invertTree($root->right);
        $tmp = $root->left;
        $root->left = $root->right;
        $root->right = $tmp;
        return $root;
    }
}
```