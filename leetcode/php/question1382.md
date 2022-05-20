```
给你一棵二叉搜索树，请你返回一棵 平衡后 的二叉搜索树，新生成的树应该与原来的树有着相同的节点值。如果有多种构造方法，请你返回任意一种。
如果一棵二叉搜索树中，每个节点的两棵子树高度差不超过 1 ，我们就称这棵二叉搜索树是 平衡的 。

示例 1：
输入：root = [1,null,2,null,3,null,4,null,null]
输出：[2,1,3,null,null,null,4]
解释：这不是唯一的正确答案，[3,1,4,null,2,null,null] 也是一个可行的构造方案。

示例 2：
输入: root = [2,1,3]
输出: [2,1,3]
 
提示：
树节点的数目在 [1, 104] 范围内。
1 <= Node.val <= 105
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
     * @return TreeNode
     */
    function balanceBST($root) {
        $result = [];
        $this->inorder($root, $result);
        return $this->buildBalance($result);
    }

    function buildBalance($result) {
        if (empty($result)) {
            return;
        }
        $mid = floor(count($result) / 2);
        $new_root = new TreeNode($result[$mid]);
        $left = array_slice($result, 0, $mid);
        $right = array_slice($result, $mid + 1, count($result) - 1);
        $lefttree = $this->buildBalance($left);
        $righttree = $this->buildBalance($right);
        $new_root->left = $lefttree;
        $new_root->right = $righttree;
        return $new_root;
    }

    function inorder($root, &$result) {
        if ($root == null) {
            return;
        }
        $this->inorder($root->left, $result);
        $result[] = $root->val;
        $this->inorder($root->right, $result);
    }
}
```