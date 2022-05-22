```
给你两棵二叉树 root 和 subRoot 。检验 root 中是否包含和 subRoot 具有相同结构和节点值的子树。如果存在，返回 true ；否则，返回 false 。

二叉树 tree 的一棵子树包括 tree 的某个节点和这个节点的所有后代节点。tree 也可以看做它自身的一棵子树。

示例 1：
输入：root = [3,4,5,1,2], subRoot = [4,1,2]
输出：true

示例 2：
输入：root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
输出：false
 
提示：
root 树上的节点数量范围是 [1, 2000]
subRoot 树上的节点数量范围是 [1, 1000]
-104 <= root.val <= 104
-104 <= subRoot.val <= 104
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
     * @param TreeNode $subRoot
     * @return Boolean
     */
    function isSubtree($root, $subRoot) {
        if ($root == null && $subRoot == null) {
            return true;
        }
        if ($root == null || $subRoot == null) {
            return false;
        }

        return $this->isSub($root, $subRoot) || $this->isSubtree($root->left, $subRoot) || $this->isSubtree($root->right, $subRoot);
    }

    function isSub($root, $subRoot) {
        if ($root == null && $subRoot == null) {
            return true;
        }
        if ($root == null || $subRoot == null) {
            return false;
        }
        return $root->val == $subRoot->val && $this->isSub($root->left, $subRoot->left) && $this->isSub($root->right, $subRoot->right);
    }
}
```