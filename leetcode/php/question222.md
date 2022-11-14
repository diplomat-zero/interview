```
给你一棵 完全二叉树 的根节点 root ，求出该树的节点个数。
完全二叉树 的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2h 个节点。

示例 1：
输入：root = [1,2,3,4,5,6]
输出：6

示例 2：
输入：root = []
输出：0

示例 3：
输入：root = [1]
输出：1
 
提示：
树中节点的数目范围是[0, 5 * 104]
0 <= Node.val <= 5 * 104
题目数据保证输入的树是 完全二叉树
 
进阶：遍历树来统计节点是一种时间复杂度为 O(n) 的简单解决方案。你可以设计一个更快的算法吗？
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
 *     function __construct($val = 0, $left = null, $right = null) {
 *         $this->val = $val;
 *         $this->left = $left;
 *         $this->right = $right;
 *     }
 * }
 */
class Solution {

    /**
     * @param TreeNode $root
     * @return Integer
     */
    function countNodes($root) {
        if ($root == null) {
            return 0;
        }
        $left_level = $this->level($root->left);
        $right_level = $this->level($root->right);
        if ($left_level == $right_level) {
            return $this->countNodes($root->right) + (1 << $left_level);
        } else {
            return $this->countNodes($root->left) + (1 << $right_level);
        }
    }

    function level($root) {
        $res = 0;
        while ($root != null) {
            $root = $root->left;
            $res++;
        }
        return $res;
    }
}
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
    function countNodes($root) {
        if ($root == null) {
            return 0;
        }
        return self::countNodes($root->left) + self::countNodes($root->right) + 1;
    }
}
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
    function countNodes($root) {
        if ($root == null) {
            return 0;
        }
        $num = 0;
        self::preOrder($root, $num);
        return $num;
    }

    function preOrder($root, &$num) {
        if ($root == null) {
            return;
        }
        $num++;
        self::preOrder($root->left, $num);
        self::preOrder($root->right, $num);
    }
}
```