```
给定一个二叉树，返回其节点值自底向上的层序遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其自底向上的层序遍历为：

[
  [15,7],
  [9,20],
  [3]
]
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
     * @return Integer[][]
     */
    function levelOrderBottom($root) {
        $result = [];

        if ($root == null) {
            return $result;
        }

        $tree_list = [];
        array_push($tree_list, [$root, 0]);
        while(!empty($tree_list)) {
            $node = array_shift($tree_list);
            $result[$node[1]][] = $node[0]->val;
            if ($node[0]->left != null) {
                array_push($tree_list, [$node[0]->left, $node[1] + 1]);
            }
            if ($node[0]->right != null) {
                array_push($tree_list, [$node[0]->right, $node[1] + 1]);
            }
        }

        return array_reverse($result);
    }
}
```