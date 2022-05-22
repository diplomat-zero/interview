```
给你二叉树的根节点 root ，请你采用前序遍历的方式，将二叉树转化为一个由括号和整数组成的字符串，返回构造出的字符串。

空节点使用一对空括号对 "()" 表示，转化后需要省略所有不影响字符串与原始二叉树之间的一对一映射关系的空括号对。

示例 1：
输入：root = [1,2,3,4]
输出："1(2(4))(3)"
解释：初步转化后得到 "1(2(4)())(3()())" ，但省略所有不必要的空括号对后，字符串应该是"1(2(4))(3)" 。

示例 2：
输入：root = [1,2,3,null,4]
输出："1(2()(4))(3)"
解释：和第一个示例类似，但是无法省略第一个空括号对，否则会破坏输入与输出一一映射的关系。
 
提示：
树中节点的数目范围是 [1, 104]
-1000 <= Node.val <= 1000
```

```
我们先明确 tree2str 函数的定义，然后利用这个定义生成左右子树的字符串，然后结合 root 组装出最后结果。

注意，题目说按照前序遍历的方式组装字符串，但我们必须在后序遍历位置去组装，因为只有那里你才能拿到左右子树的字符串。
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
     * @return String
     */
    function tree2str($root) {
        if ($root == null) {
            return '';
        }
        if ($root->left == null && $root->right == null) {
            return (string)$root->val ;
        }

        $left = $this->tree2str($root->left);
        $right = $this->tree2str($root->right);

        if ($root->left != null && $root->right == null) {
            return $root->val . '(' . $left . ')'; 
        }
        if ($root->left == null && $root->right != null) {
            return $root->val . '()' . '(' . $right . ')';
        }
        return $root->val . '(' . $left . ')' . '(' . $right . ')';
    }
}
```