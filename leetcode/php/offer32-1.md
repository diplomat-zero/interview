```
从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回：
[3,9,20,15,7]
 
提示：
节点总数 <= 1000
```

```
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($value) { $this->val = $value; }
 * }
 */
class Solution {

    /**
     * @param TreeNode $root
     * @return Integer[]
     */
    function levelOrder($root) {
        $ret = [];
        if ($root == null) {
            return $ret;
        }

        $queue = [];
        $queue[] = $root;
        while (!empty($queue)) {
            $node = array_shift($queue);
            $ret[] = $node->val;
            if (!empty($node->left)) {
                $queue[] = $node->left;
            }
            if (!empty($node->right)) {
                $queue[] = $node->right;
            }
        }

        return $ret;
    }
}
```