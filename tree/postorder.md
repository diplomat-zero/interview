```
二叉树的后序遍历的记忆法则是“左右根"，即先遍历左子树节点，再遍历右子树节点，最后遍历根节点。
```

```
php
```

```
function postorder($root)
    {
        $result = [];
        $stack[] = $root;

        while (!empty($stack)) {
            $top = end($stack);
            array_pop($stack);
            $result[] = $top->val;

            if ($top->left != null) {
                array_push($stack, $top->left);
            }
            if ($top->right != null) {
                array_push($stack, $top->right);
            }
        }

        return array_reverse($result);
    }
```