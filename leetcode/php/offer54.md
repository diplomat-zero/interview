```
给定一棵二叉搜索树，请找出其中第 k 大的节点的值。

示例 1:
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4

示例 2:
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
 
限制：
1 ≤ k ≤ 二叉搜索树元素个数
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
 *     function __construct($value) { $this->val = $value; }
 * }
 */
class Solution {

    /**
     * @param TreeNode $root
     * @param Integer $k
     * @return Integer
     */
    public $k;
    function kthLargest($root, $k) {
        $res = 0;
        $this->k = $k;
        $this->inorder($root, $res);
        return $res;
    }

    function inorder($root, &$res) {
        if ($root == null) {
            return;
        }
        $this->inorder($root->right, $res);
        if ($this->k == 0) {
            return;
        }
        if (--$this->k == 0) {
            $res = $root->val;
            return;
        }
        $this->inorder($root->left, $res);
    }
}
```