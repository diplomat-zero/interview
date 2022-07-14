```
给定一个二叉树，返回其节点值的锯齿形层序遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

例如：
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回锯齿形层序遍历如下：

[
  [3],
  [20,9],
  [15,7]
]
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
     * @return Integer[][]
     */
    function zigzagLevelOrder($root) {
        if ($root == null) {
            return [];
        }
        $stack[] = $root;
        $result = [];
        $i = 0;
        while (!empty($stack)) {
            $len = count($stack);
            $tmp = [];
            for ($j = 0; $j < $len; $j++) {
                $node = array_shift($stack);
                if ($i % 2 == 0) {
                    $tmp[] = $node->val;
                } else {
                    array_unshift($tmp, $node->val);
                }
                if ($node->left) {
                    $stack[] = $node->left;
                }

                if ($node->right) {
                    $stack[] = $node->right;
                }
            }
            $result[] = $tmp;
            $i++;
        }
        return $result;
    }
}
```

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

$tree0 = new TreeNode(0);
$tree1 = new TreeNode(1);
$tree2 = new TreeNode(2);
$tree3 = new TreeNode(3);
$tree4 = new TreeNode(4);
$tree5 = new TreeNode(5);
$tree6 = new TreeNode(6);
$tree0->left = $tree1;
$tree0->right = $tree2;
$tree1->left = $tree3;
$tree1->right = $tree4;
$tree2->left = $tree5;
$tree2->right = $tree6;

$so = new Solution();
$ret = $so->zigzagLevelOrder($tree0);
print_r($ret);
```