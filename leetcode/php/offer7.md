```
输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。
假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

示例 1:
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]

示例 2:
Input: preorder = [-1], inorder = [-1]
Output: [-1]
 
限制：
0 <= 节点个数 <= 5000
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
     * @param Integer[] $preorder
     * @param Integer[] $inorder
     * @return TreeNode
     */
    function buildTree($preorder, $inorder) {
        if (count($preorder) == 0 || count($inorder) == 0) {
            return null;
        }

        $find = 0;
        for ($i = 0; $i < count($inorder); $i++) {
            if ($inorder[$i] == $preorder[0]) {
                $find = $i;
                break;
            }
        }

        $leftinorder = array_slice($inorder, 0, $find);
        $rightinorder = array_slice($inorder, $find + 1, count($inorder) - $find - 1);
        
        $leftpreorder = array_slice($preorder, 1, count($leftinorder));
        $rightpreorder = array_slice($preorder, count($leftinorder) + 1, count($preorder) - count($leftinorder));

        $root = new TreeNode($preorder[0]);
        $root->left = $this->buildTree($leftpreorder, $leftinorder);
        $root->right = $this->buildTree($rightpreorder, $rightinorder);

        return $root;
    }
}
```