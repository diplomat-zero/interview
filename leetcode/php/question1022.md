```
给出一棵二叉树，其上每个结点的值都是 0 或 1 。每一条从根到叶的路径都代表一个从最高有效位开始的二进制数。例如，如果路径为 0 -> 1 -> 1 -> 0 -> 1，那么它表示二进制数 01101，也就是 13 。

对树上的每一片叶子，我们都要找出从根到该叶子的路径所表示的数字。

返回这些数字之和。题目数据保证答案是一个 32 位 整数。

 

示例 1：


输入：root = [1,0,1,0,1,0,1]
输出：22
解释：(100) + (101) + (110) + (111) = 4 + 5 + 6 + 7 = 22
示例 2：

输入：root = [0]
输出：0
示例 3：

输入：root = [1]
输出：1
示例 4：

输入：root = [1,1]
输出：3
 

提示：

树中的结点数介于 1 和 1000 之间。
Node.val 为 0 或 1 。
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
     * @return Integer
     */
    function sumRootToLeaf($root) {
        $result = 0;
        $trace = 0;
        self::dfs($root, $trace, $result);
        return $result;
    }

    function dfs($root, $trace, &$result)
    {
        if ($root == null) {
            return;
        }

        $trace = $trace << 1;
        $trace += $root->val;
        if ($root->left == null && $root->right == null) {
            $result += $trace;
            return;
        }

        self::dfs($root->left, $trace, $result);
        self::dfs($root->right, $trace, $result);
    }
}
```