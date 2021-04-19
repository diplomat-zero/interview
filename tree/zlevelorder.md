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
    function zigzagLevelOrder($root) {
        $result = [];

        if ($root == null) {
            return $result;
        }

        $tree_list = [];
        array_push($tree_list, [$root, 0]);
        while(!empty($tree_list)) {
            $node = array_shift($tree_list);
            if ($node[1] % 2 == 0) {
                $result[$node[1]][] = $node[0]->val;
            } else {
                if (isset($result[$node[1]])) {
                    array_unshift($result[$node[1]], $node[0]->val);
                } else {
                    $result[$node[1]][] = $node[0]->val;
                }
            }
            if ($node[0]->left != null) {
                array_push($tree_list, [$node[0]->left, $node[1] + 1]);
            }
            if ($node[0]->right != null) {
                array_push($tree_list, [$node[0]->right, $node[1] + 1]);
            }
        }

        return $result; 
    }
}
```