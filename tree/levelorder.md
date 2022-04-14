```
<?php
  class TreeNode {
      public $val = null;
      public $left = null;
      public $right = null;
      function __construct($value) { $this->val = $value; }
  }

class Solution {

    /**
     * @param TreeNode $root
     * @return Integer[][]
     */
    function levelOrder($root) {
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
                $tree_list[] = [$node[0]->left, $node[1] + 1];
            }
            if ($node[0]->right != null) {
                $tree_list[] = [$node[0]->right, $node[1] + 1];
            }
        }

        return $result;
    }
}
```