```
从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]
 

提示：

节点总数 <= 1000
```

```

```

```
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func levelOrder(root *TreeNode) [][]int {
    res := make([][]int, 0)
    if root == nil {
        return res
    }
    stack := make([]*TreeNode, 0)
    stack = append(stack, root)
    for len(stack) > 0 {
        length := len(stack)
        tmp := make([]int, 0)
        for i := 0; i < length; i++ {
            node := stack[0]
            stack = stack[1:]
            if node.Left != nil {
                stack = append(stack, node.Left)
            }
            if node.Right != nil {
                stack = append(stack, node.Right)
            }
            tmp = append(tmp, node.Val)
        }
        res = append(res, tmp)
    }
    return res
}
```