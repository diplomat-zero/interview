```
给你二叉搜索树的根节点 root ，该树中的 恰好 两个节点的值被错误地交换。请在不改变其结构的情况下，恢复这棵树 。

示例 1：
输入：root = [1,3,null,null,2]
输出：[3,1,null,null,2]
解释：3 不能是 1 的左孩子，因为 3 > 1 。交换 1 和 3 使二叉搜索树有效。

示例 2：
输入：root = [3,1,4,null,null,2]
输出：[2,1,4,null,null,3]
解释：2 不能在 3 的右子树中，因为 2 < 3 。交换 2 和 3 使二叉搜索树有效。
 
提示：
树上节点的数目在范围 [2, 1000] 内
-231 <= Node.val <= 231 - 1
 
进阶：使用 O(n) 空间复杂度的解法很容易实现。你能想出一个只使用 O(1) 空间的解决方案吗？
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
     * @return NULL
     */
    public $first;
    public $second;
    public $pre;
    function recoverTree($root) {
        $this->pre = new TreeNode(PHP_INT_MIN);
        $this->inorder($root);

        $tmp = $this->first->val;
        $this->first->val = $this->second->val;
        $this->second->val = $tmp;
    }

    function inorder($root) {
        if ($root == null) {
            return;
        }
        $this->inorder($root->left);
        if ($root->val < $this->pre->val) {
            if ($this->first == null) {
                $this->first = $this->pre;
            }
            $this->second = $root;
        }
        $this->pre = $root;
        $this->inorder($root->right);
    }
}
```