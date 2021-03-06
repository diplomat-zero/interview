```
给定一个二叉树的根节点 root ，返回它的 中序 遍历。

示例 1：
输入：root = [1,null,2,3]
输出：[1,3,2]

示例 2：
输入：root = []
输出：[]

示例 3：
输入：root = [1]
输出：[1]

示例 4：
输入：root = [1,2]
输出：[2,1]

示例 5：
输入：root = [1,null,2]
输出：[1,2]
 
提示：

树中节点数目在范围 [0, 100] 内
-100 <= Node.val <= 100
 
进阶: 递归算法很简单，你可以通过迭代算法完成吗
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
     * @return Integer[]
     */
    function inorderTraversal($root) {
        $nums = [];
        $this->inorder($root, $nums);
        return $nums;
    }

    function inorder($root, &$nums) {
        if ($root == null) {
            return;
        }
        $this->inorder($root->left, $nums);
        $nums[] = $root->val;
        $this->inorder($root->right, $nums);
    }
}
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
     * @return Integer[]
     */
    function inorderTraversal($root) {
        $nums = [];
        $stack = array();
        $center_node = $root;
        while (!empty($stack) || $center_node != null) {
            while ($center_node != null) {
                array_push($stack, $center_node);
                $center_node = $center_node->left;
            }

            $center_node = array_pop($stack);
            $nums[] = $center_node->val;

            $center_node = $center_node->right;
        }

        return $nums;
    }
}
```