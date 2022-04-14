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