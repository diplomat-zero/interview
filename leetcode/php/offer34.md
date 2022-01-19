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
     * @param Integer $target
     * @return Integer[][]
     */
    function pathSum($root, $target) {
        if ($root == null) {
            return [];
        }
        $result = [];
        $trace = [$root];
        $this->dfs($root, $target, $result, $trace);
        return $result;
    }

    function dfs($root, $target, &$result, &$trace) {
        if ($root->left == null && $root->right == null) {
            foreach ($trace as $value) {
                $sum += $value->val;
                $tmp[] = $value->val;
            }
            if ($sum == $target) {
                $result[] = $tmp;
            }
            return;
        }

        if ($root->left != null && !in_array($root->left, $trace)) {
            array_push($trace, $root->left);
            $this->dfs($root->left, $target, $result, $trace);
            array_pop($trace);
        }

        if ($root->right != null && !in_array($root->right, $trace)) {
            array_push($trace, $root->right);
            $this->dfs($root->right, $target, $result, $trace);
            array_pop($trace);
        }
    }
}
```