```
给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

示例：
二叉树：[3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层序遍历结果：

[
  [3],
  [9,20],
  [15,7]
]
```

```
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
     * @return Integer[][]
     */
    function levelOrder($root) {
        $result = [];

        if ($root == null) {
            return $result;
        }

        $queue = new SplQueue();
        $queue->enqueue([$root, 0]);
        while (!$queue->isEmpty()) {
            $node = $queue->dequeue();
            $result[$node[1]][] = $node[0]->val;
            if ($node[0]->left) {
                $queue->enqueue([$node[0]->left, $node[1] + 1]);
            }
            if ($node[0]->right) {
                $queue->enqueue([$node[0]->right, $node[1] + 1]);
            }
        }

        return $result;
    }
}
```