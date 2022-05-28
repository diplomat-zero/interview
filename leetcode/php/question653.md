```
给定一个二叉搜索树 root 和一个目标结果 k，如果 BST 中存在两个元素且它们的和等于给定的目标结果，则返回 true。

示例 1：
输入: root = [5,3,6,2,4,null,7], k = 9
输出: true

示例 2：
输入: root = [5,3,6,2,4,null,7], k = 28
输出: false
 
提示:
二叉树的节点个数的范围是  [1, 104].
-104 <= Node.val <= 104
root 为二叉搜索树
-105 <= k <= 105
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
     * @param Integer $k
     * @return Boolean
     */
    function findTarget($root, $k) {
        $result = [];
        $this->inorder($root, $result);
        $left = 0;
        $right = count($result) - 1;
        while ($left < $right) {
            $sum = $result[$left] + $result[$right];
            if ($sum == $k) {
                return true;
            } else if ($sum > $k) {
                $right--;
            } else {
                $left++;
            }
        }
        return false;
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