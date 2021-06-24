```
给定一个二叉树，返回所有从根节点到叶子节点的路径。
说明: 叶子节点是指没有子节点的节点。

示例:
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]
解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
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
     * @return String[]
     */
    function binaryTreePaths($root) {
        $result = [];
        self::dfs($root, [$root], $result);
        return $result;
    }

    function dfs($root, $trace, &$result) {
        if ($root->left == null && $root->right == null) {
            $tmp = '';
            foreach($trace as $key => $val) {
                $tmp .= $val->val;
                if ($key < count($trace) - 1) {
                    $tmp .= '->';
                }
            }
            $result[] = $tmp;
        }
        if ($root->left != null) {
            if (!in_array($root->left, $trace)) {
                array_push($trace, $root->left);
                self::dfs($root->left, $trace, $result);
                array_pop($trace);
            }
        }
        if ($root->right != null) {
            if (!in_array($root->right, $trace)) {
                array_push($trace, $root->right);
                self::dfs($root->right, $trace, $result);
                array_pop($trace);
            }
        }
    }
}
```