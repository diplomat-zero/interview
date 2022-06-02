```
给出二叉树的根节点 root，树上每个节点都有一个不同的值。
如果节点值在 to_delete 中出现，我们就把该节点从树上删去，最后得到一个森林（一些不相交的树构成的集合）。
返回森林中的每棵树。你可以按任意顺序组织答案。

示例 1：
输入：root = [1,2,3,4,5,6,7], to_delete = [3,5]
输出：[[1,2,null,4],[6],[7]]

示例 2：
输入：root = [1,2,4,null,3], to_delete = [3]
输出：[[1,2,4]]
 
提示：
树中的节点数最大为 1000。
每个节点都有一个介于 1 到 1000 之间的值，且各不相同。
to_delete.length <= 1000
to_delete 包含一些从 1 到 1000、各不相同的值。
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
     * @param Integer[] $to_delete
     * @return TreeNode[]
     */
    function delNodes($root, $to_delete) {
        $res = [];
        $this->toDel($root, $to_delete, false, $res);
        return $res;
    }

    function toDel($root, $to_delete, $has_parent, &$res) {
        if ($root == null) {
            return null;
        }

        $delete = in_array($root->val, $to_delete);
        if (!$delete && !$has_parent) {
            $res[] = $root;
        }

        $root->left = $this->toDel($root->left, $to_delete, !$delete, $res);
        $root->right = $this->toDel($root->right, $to_delete, !$delete, $res);
        return $delete ? null : $root;
    }
}
```