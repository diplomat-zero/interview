```
根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
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
     * @param Integer[] $preorder
     * @param Integer[] $inorder
     *
     * @return TreeNode
     */
    function buildTree($preorder, $inorder) {
        if (empty($preorder)) {
            return null;
        }
        $root_node = new TreeNode($preorder[0]);

        for ($i = 0; $i < count($inorder); $i++) {
            if ($inorder[$i] == $preorder[0]) {
                $find = $i;
                break;
            }
        }

        $left_preorder = $right_preorder = $left_inorder = $right_inorder = [];
        $left = 0;
        for ($m = 1; $m < count($preorder); $m++) {
            if  ($left < $find) {
                $left_preorder[] = $preorder[$m];
            } else {
                $right_preorder[] = $preorder[$m];
            }
            $left++;
        }

        for ($n = 0; $n < count($inorder); $n++) {
            if ($n < $find) {
                $left_inorder[] = $inorder[$n];
            } elseif ($n > $find) {
                $right_inorder[] = $inorder[$n];
            }
        }

        $root_node->left = $this->buildTree($left_preorder, $left_inorder);
        $root_node->right = $this->buildTree($right_preorder, $right_inorder);
        return $root_node;
    }
}
```