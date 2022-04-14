```
二叉树的前序遍历的记忆法则是“根左右"，即先遍历根节点，再遍历左子树节点，再遍历右子树节点。
```

```
php
```

```
    function preOrder($root)
    {
        $result = [];
        $stack[] = $root;

        while (!empty($stack)) {
            $top = end($stack);
            array_pop($stack);

            $result[] = $top->val;
            if ($top->right != null) {
                array_push($stack, $top->right);
            }
            if ($top->left != null) {
                array_push($stack, $top->left);
            }
        }

        return $result;
    }
```