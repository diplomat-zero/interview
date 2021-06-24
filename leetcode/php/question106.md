```
根据一棵树的中序遍历与后序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出
中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]
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
     * @param Integer[] $inorder
     * @param Integer[] $postorder
     *
     * @return TreeNode
     */
    function buildTree($inorder, $postorder) {
        if (empty($postorder)) {
            return;
        }

        $root = $postorder[count($postorder) - 1];
        $root_node = new TreeNode($root);

        for ($i = 0; $i < count($inorder); $i++) {
            if ($inorder[$i] == $root) {
                break;
            }
        }

        $left_inorder = $right_inorder = $left_postorder = $right_postorder = [];

        $post = 0;
        for ($m = 0; $m < count($postorder) - 1; $m++) {
            if ($post < $i) {
                $left_postorder[] = $postorder[$m];
            } else {
                $right_postorder[] = $postorder[$m];
            }
            $post++;
        }

        for ($n = 0; $n < count($inorder); $n++) {
            if ($n < $i) {
                $left_inorder[] = $inorder[$n];
            } elseif ($n > $i) {
                $right_inorder[] = $inorder[$n];
            }
        }
        $root_node->left = $this->buildTree($left_inorder, $left_postorder);
        $root_node->right = $this->buildTree($right_inorder, $right_postorder);
        return $root_node;
    }
}
```