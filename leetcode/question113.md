```
给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径。
叶子节点 是指没有子节点的节点。

示例 1：
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]

示例 2：
输入：root = [1,2,3], targetSum = 5
输出：[]

示例 3：
输入：root = [1,2], targetSum = 0
输出：[]
 
提示：
树中节点总数在范围 [0, 5000] 内
-1000 <= Node.val <= 1000
-1000 <= targetSum <= 1000
```

```

```

```
待优化
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
     * @param Integer $targetSum
     * @return Integer[][]
     */
    function pathSum($root, $targetSum) {
        $result = [];
        if ($root == null) {
            return $result;
        }
        self::trace($root, [$root], $targetSum, $result);
        return $result;
    }

    function trace($tree, $tracek, $targetSum, &$result) {
        if ($tree->left == null && $tree->right == null) {
            $sum = 0;
            foreach($tracek as $value) {
                $sum += $value->val;
                $tmp[] = $value->val;
            }
            if ($sum == $targetSum) {
                $result[] = $tmp;
            }            
        }
        if ($tree->left != null) {
            if (!in_array($tree->left, $tracek)) {
                $tracek[] = $tree->left;
                self::trace($tree->left, $tracek, $targetSum, $result);
                array_pop($tracek);
            }
        }
        if ($tree->right != null) {
            if (!in_array($tree->right, $tracek)) {
                $tracek[] = $tree->right;
                self::trace($tree->right, $tracek, $targetSum, $result);
                array_pop($tracek);
            }
        }
    }
}
```