```
给你二叉树的根结点 root ，请你将它展开为一个单链表：
展开后的单链表应该同样使用 TreeNode ，其中 right 子指针指向链表中下一个结点，而左子指针始终为 null 。
展开后的单链表应该与二叉树 先序遍历 顺序相同。

示例 1：
输入：root = [1,2,5,3,4,null,6]
输出：[1,null,2,null,3,null,4,null,5,null,6]

示例 2：
输入：root = []
输出：[]

示例 3：
输入：root = [0]
输出：[0]
 
提示：
树中结点数在范围 [0, 2000] 内
-100 <= Node.val <= 100
 
进阶：你可以使用原地算法（O(1) 额外空间）展开这棵树吗？
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
     * @return NULL
     */
    function flatten($root) {
        $pre = null;
        $stack[] = $root;
        while (!empty($stack)) {
            $node = end($stack);
            array_pop($stack);

            if ($pre != null) {
                $pre->right = $node;
                $pre->left = null;
            }

            if ($node->right != null) {
                $stack[] = $node->right;
            }

            if ($node->left != null) {
                $stack[] = $node->left;
            }

            $pre = $node;
        }
    }
}
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
     * @return NULL
     */
    function flatten($root) {
        $result = [];
        $this->inorder($root, $result);
        for ($i = 0; $i < count($result) - 1; $i++) {
            $result[$i]->right = $result[$i + 1];
            $result[$i]->left = null;
        }
        return $root;
    }

    function inorder($root, &$result) {
        if ($root == null) {
            return;
        }
        $result[] = $root;
        $this->inorder($root->left, $result);
        $this->inorder($root->right, $result);
    }
}
```