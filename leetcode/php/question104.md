```
给定一个二叉树，找出其最大深度。
二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。
说明: 叶子节点是指没有子节点的节点。

示例：
给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。
```

```
class TreeNode {
    public $val = null;

    public $left = null;

    public $right = null;

    function __construct($val = 0, $left = null, $right = null) {
        $this->val = $val;
        $this->left = $left;
        $this->right = $right;
    }
}
class Solution {
    /**
     * @param TreeNode $root
     *
     * @return Integer
     */
    function maxDepth($root) {
        if ($root == null) {
            return 0;
        }
        $left = $this->maxDepth($root->left);
        $right = $this->maxDepth($root->right);
        return $left > $right ? $left + 1 : $right + 1;
    }
}
```