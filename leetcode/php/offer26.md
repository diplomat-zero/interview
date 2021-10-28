```
输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)
B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

     3
    / \
   4   5
  / \
 1   2
给定的树 B：

   4 
  /
 1
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

示例 1：
输入：A = [1,2,3], B = [3,1]
输出：false

示例 2：
输入：A = [3,4,5,1,2], B = [4,1]
输出：true

限制：
0 <= 节点个数 <= 10000
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
     * @param TreeNode $A
     * @param TreeNode $B
     * @return Boolean
     */
    function isSubStructure($A, $B) {
        if ($A == null && $B == null) {
            return true;
        }

        if ($A == null || $B == null) {
            return false;
        }

        return $this->isSub($A, $B) || $this->isSubStructure($A->left, $B) || $this->isSubStructure($A->right, $B);
    }

    function isSub($A, $B) {
        if ($B == null) {
            return true;
        }

        if ($A == null) {
            return false;
        }

        if ($A->val == $B->val) {
            return $this->isSub($A->left, $B->left) && $this->isSub($A->right, $B->right);
        }

        return false;
    }
}
```