```
给定一棵二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。
示例:

输入: [1,2,3,null,5,null,4]
输出: [1, 3, 4]
解释:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
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
     * @return Integer[]
     */
    function rightSideView($root) {
        if ($root == null) {
            return [];
        }
        $stack[] = $root;
        $result = [];
        while (!empty($stack)) {
            $len = count($stack);
            $tmp = [];
            for ($i = 0; $i < $len; $i++) {
                $node = array_shift($stack);
                $tmp[] = $node->val;
                if ($node->left) {
                    $stack[] = $node->left;
                }
                if ($node->right) {
                    $stack[] = $node->right;
                }
            }
            $result[] = end($tmp);
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
      function __construct($val = 0, $left = null, $right = null) {
          $this->val = $val;
          $this->left = $left;
          $this->right = $right;
      }
  }

class Solution {

    /**
     * @param TreeNode $root
     * @return Integer[]
     */
    function rightSideView($root) {
        $res = [];
        if ($root == null) {
            return $res;
        }
        $result = self::levelOrder($root);
        foreach ($result as $val) {
            $res[] = array_pop($val);
        }

        return $res;
    }

    function levelOrder($root) {
        $queue = $result = [];
        array_push($queue, [$root, 0]);
        while (!empty($queue)) {
            $node = array_shift($queue);
            $result[$node[1]][] = $node[0]->val;
            if ($node[0]->left != null) {
                array_push($queue, [$node[0]->left, $node[1] + 1]);
            }
            if ($node[0]->right != null) {
                array_push($queue, [$node[0]->right, $node[1] + 1]);
            }
        }

        return $result;
    }
}
```