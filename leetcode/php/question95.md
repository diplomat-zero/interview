```
给定一个整数 n，生成所有由 1 ... n 为节点所组成的 二叉搜索树 。

示例：
输入：3
输出：
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释：
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
 

提示：
0 <= n <= 8
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
     * @param Integer $n
     *
     * @return TreeNode[]
     */
    function generateTrees($n) {
        return $this->erCha(1, $n);
    }

    function erCha($left, $right) {
        $ret = [];
        if ($left > $right) {
            $ret[] = null;
            return $ret;
        }
        for ($i = $left; $i <= $right; $i++) {
            $left_tree = $this->erCha($left, $i - 1);
            $right_tree = $this->erCha($i + 1, $right);
            foreach  ($left_tree as $left_val) {
                foreach ($right_tree as $right_val) {
                    $new = new TreeNode($i);
                    $new->right = $right_val;
                    $new->left = $left_val;
                    $ret[] = $new;
                }
            }
        }

        return $ret;
    }
}
```