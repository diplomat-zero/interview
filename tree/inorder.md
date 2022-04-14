```
二叉树的中序遍历的记忆法则是“左根右"，即先遍历左子树节点，再遍历根节点，再遍历右子树节点。
```

```
php
```

```
    function inorder($root)
    {
        $result = [];
        $stack = [];
        $cur = $root;

        while (!empty($stack) || $cur != null) {
            while ($cur != null) {
                array_push($stack, $cur);
                $cur = $cur->left;
            }

            $top = end($stack);
            array_pop($stack);
            $result[] = $top->val;

            $cur = $top->right;
        }

        return $result;
    }
```