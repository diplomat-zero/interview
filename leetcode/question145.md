```
给定一个二叉树，返回它的 后序 遍历。

示例:

输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [3,2,1]
进阶: 递归算法很简单，你可以通过迭代算法完成吗？
```

```
class Solution {
    /**
     * @param TreeNode $root
     *
     * @return Integer[]
     */
    function postorderTraversal($root) {
        $nums = [];
        $this->post($root, $nums);
        return $nums;
    }

    function post($tree, &$nums) {
        if ($tree == null) {
            return;
        }
        $this->post($tree->left, $nums);
        $this->post($tree->right, $nums);
        $nums[] = $tree->val;
    }
}
```