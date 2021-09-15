```
给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

结点左子树中所含结点的值小于等于当前结点的值
结点右子树中所含结点的值大于等于当前结点的值
左子树和右子树都是二叉搜索树
例如：
给定 BST [1,null,2,2],

   1
    \
     2
    /
   2
返回[2].

提示：如果众数超过1个，不需考虑输出顺序

进阶：你可以不使用额外的空间吗？（假设由递归产生的隐式调用栈的开销不被计算在内）
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
     * @return Integer[]
     */
    function findMode($root) {
        $ret = [];
        self::inorder($root, $ret);

        $res = [];
        foreach($ret as $k => $v) {
            if (count($res) == 0) {
                $res[] = $k;
                $max = $v;
            } else {
                if ($v > $max) {
                    $res = [];
                    $res[] = $k;
                    $max = $v;
                } elseif ($max == $v) {
                    $res[] = $k;
                }
            }
        }

        return $res;
    }

    function inorder($root, &$ret) {
        if ($root == null) {
            return;
        }

        self::inorder($root->left, $ret);
        if (isset($ret[$root->val])) {
            $ret[$root->val]++;
        } else {
            $ret[$root->val] = 1;
        }

        self::inorder($root->right, $ret);
    }
}
```