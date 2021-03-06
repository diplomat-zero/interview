```
给定两个二叉树，编写一个函数来检验它们是否相同。
如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

示例 1:
输入:       1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]
输出: true

示例 2:
输入:      1          1
          /           \
         2             2

        [1,2],     [1,null,2]
输出: false

示例 3:
输入:       1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]
输出: false
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
     * @param TreeNode $p
     * @param TreeNode $q
     *
     * @return Boolean
     */
    function isSameTree($p, $q) {
        if ($p == null && $q == null) {
            return true;
        }

        if ($p == null || $q == null) {
            return false;
        }

        return $p->val == $q->val && $this->isSameTree($p->left, $q->left) && $this->isSameTree($p->right, $q->right);
    }
}
```