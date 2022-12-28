```
给定一个二叉树的 根节点 root，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

 

示例 1:



输入: [1,2,3,null,5,null,4]
输出: [1,3,4]
示例 2:

输入: [1,null,3]
输出: [1,3]
示例 3:

输入: []
输出: []
 

提示:

二叉树的节点个数的范围是 [0,100]
-100 <= Node.val <= 100 
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
func rightSideView(root *TreeNode) []int {
    if root == nil {
        return []int{}
    }
    res := make([]int, 0)
    stack := make([]*TreeNode, 0)
    stack = append(stack, root)
    for len(stack) != 0 {
        length := len(stack)
        tmp := make([]int, 0)
        for i := 0; i < length; i++ {
            node := stack[0]
            stack = stack[1:]
            tmp = append(tmp, node.Val)
            if node.Left != nil {
                stack = append(stack, node.Left)
            }
            if node.Right != nil {
                stack = append(stack, node.Right)
            }
        }
        res = append(res, tmp[len(tmp) - 1])
    }
    return res
}
```