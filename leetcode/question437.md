```
给定一个二叉树，它的每个结点都存放着一个整数值。
找出路径和等于给定数值的路径总数。
路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。
二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。

示例：
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:
1.  5 -> 3
2.  5 -> 2 -> 1
3.  -3 -> 11
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

    public static $result = 0;
    /**
     * @param TreeNode $root
     * @param Integer $targetSum
     * @return Integer
     */
    function pathSum($root, $targetSum) {
        if ($root == null) {
            return 0;
        }
        $ret = 0;
        $ret += self::sum($root, $targetSum);
        $ret += self::pathSum($root->left, $targetSum);
        $ret += self::pathSum($root->right, $targetSum);
        return $ret;
    }

    function sum($root, $targetSum) {
        if ($root == null) {
            return 0;
        }
        
        $ret = 0;
        if ($root->val == $targetSum) {
            $ret++;
        }
        
        $ret += self::sum($root->left, $targetSum - $root->val);
        $ret += self::sum($root->right, $targetSum - $root->val);
        return $ret;
    }   
}
```