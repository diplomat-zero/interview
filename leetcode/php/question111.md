```
给定一个二叉树，找出其最小深度。
最小深度是从根节点到最近叶子节点的最短路径上的节点数量。
说明：叶子节点是指没有子节点的节点。

示例 1：
输入：root = [3,9,20,null,null,15,7]
输出：2

示例 2：
输入：root = [2,null,3,null,4,null,5,null,6]
输出：5
 
提示：
树中节点数的范围在 [0, 105] 内
-1000 <= Node.val <= 1000
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
    function minDepth($root) {
        if (empty($root)) {
            return 0;
        }
        $queue = [];
        array_push($queue, $root);
        $depth = 0;
    
        while (!empty($queue)) {
            $depth++;
            $len = count($queue);
            for ($i = 0; $i < $len; $i++) {
                $cur = array_shift($queue);

                if ($cur->left == null && $cur->right == null) {
                    return $depth;
                }
                    
                if ($cur->left != null) {
                    array_push($queue, $cur->left);
                }
                if ($cur->right != null) {
                    array_push($queue, $cur->right);
                }
            }
        }
    }
}
```