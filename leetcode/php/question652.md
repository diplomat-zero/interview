```
给定一棵二叉树 root，返回所有重复的子树。
对于同一类的重复子树，你只需要返回其中任意一棵的根结点即可。
如果两棵树具有相同的结构和相同的结点值，则它们是重复的。

示例 1：
输入：root = [1,2,3,4,null,2,4,null,null,4]
输出：[[2,4],[4]]

示例 2：
输入：root = [2,1,1]
输出：[[1]]

示例 3：
输入：root = [2,2,2,3,null,3,null]
输出：[[2,3],[3]]
 
提示：
树中的结点数在[1,10^4]范围内。
-200 <= Node.val <= 200
```

```
如果你想知道以自己为根的子树是不是重复的，是否应该被加入结果列表中，你需要知道什么信息？

你需要知道以下两点：

1、以我为根的这棵二叉树（子树）长啥样？

2、以其他节点为根的子树都长啥样？

这就叫知己知彼嘛，我得知道自己长啥样，还得知道别人长啥样，然后才能知道有没有人跟我重复，对不对？

我怎么知道自己以我为根的二叉树长啥样？前文 序列化和反序列化二叉树 其实写过了，二叉树的前序/中序/后序遍历结果可以描述二叉树的结构。

我咋知道其他子树长啥样？每个节点都把以自己为根的子树的样子存到一个外部的数据结构里即可。
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
     * @return TreeNode[]
     */
    function findDuplicateSubtrees($root) {
        $map = [];
        $res = [];
        $this->build($root, $map, $res);
        return $res;
    }

    function build($root, &$map, &$res) {
        if ($root == null) {
            return '#';
        }

        $left = $this->build($root->left, $map, $res);
        $right = $this->build($root->right, $map, $res);

        $current = $left . ',' . $right . ',' . $root->val;
        if (isset($map[$current]) && $map[$current] == 1) {
            $res[] = $root;
        }
        if (isset($map[$current])) {
            $map[$current]++;
        } else {
            $map[$current] = 1; 
        }
        
        return $current;
    }
}
```