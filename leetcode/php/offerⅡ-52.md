```
给你一棵二叉搜索树，请 按中序遍历 将其重新排列为一棵递增顺序搜索树，使树中最左边的节点成为树的根节点，并且每个节点没有左子节点，只有一个右子节点。

示例 1：
输入：root = [5,3,6,2,4,null,8,1,null,null,null,7,9]
输出：[1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9]

示例 2：
输入：root = [5,1,7]
输出：[1,null,5,null,7]
 
提示：
树中节点数的取值范围是 [1, 100]
0 <= Node.val <= 1000
```

```
思路
在中序遍历的时候，修改节点指向就可以实现。具体地，当我们遍历到一个节点时，把它的左孩子设为空，并将其本身作为上一个遍历到的节点的右孩子。这里需要有一些想象能力。递归遍历的过程中，由于递归函数的调用栈保存了节点的引用，因此上述操作可以实现。
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
    function increasingBST($root) {
        $result = new TreeNode(-1);
        $res = $result;
        $this->inorder($root, $res);
        return $result->right;
    }

    function inorder($root, &$res) {
        if ($root == null) {
            return;
        }
        $this->inorder($root->left, $res);
        $res->right = $root;
        $root->left = null;
        $res = $root;
        $this->inorder($root->right, $res);
    }
}
```