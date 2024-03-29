```
给你二叉树的根节点 root ，返回它节点值的 前序 遍历。

示例 1：
输入：root = [1,null,2,3]
输出：[1,2,3]

示例 2：
输入：root = []
输出：[]

示例 3：
输入：root = [1]
输出：[1]

示例 4：
输入：root = [1,2]
输出：[1,2]

示例 5：
输入：root = [1,null,2]
输出：[1,2]
 
提示：

树中节点数目在范围 [0, 100] 内
-100 <= Node.val <= 100
 
进阶：递归算法很简单，你可以通过迭代算法完成吗？
```

```
class Solution {
    /**
     * @param TreeNode $root
     *
     * @return Integer[]
     */
    function preorderTraversal($root) {
        $nums = [];
        $this->pre($root, $nums);
        return $nums;
    }

    function pre($tree, &$nums) {
        if ($tree == null) {
            return;
        }
        $nums[] = $tree->val;
        $this->pre($tree->left, $nums);
        $this->pre($tree->right, $nums);
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
    function preorderTraversal($root) {
        $result = [];
        $stack[] = $root;
        while (!empty($stack)) {
            $node = end($stack);
            array_pop($stack);

            $result[] = $node->val;
            if ($node->right != null) {
                $stack[] = $node->right;
            }

            if ($node->left != null) {
                $stack[] = $node->left;
            }
        }

        return $result;
    }
}
```