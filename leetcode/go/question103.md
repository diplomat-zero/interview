```
给你二叉树的根节点 root ，返回其节点值的 锯齿形层序遍历 。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

 

示例 1：


输入：root = [3,9,20,null,null,15,7]
输出：[[3],[20,9],[15,7]]
示例 2：

输入：root = [1]
输出：[[1]]
示例 3：

输入：root = []
输出：[]
 

提示：

树中节点数目在范围 [0, 2000] 内
-100 <= Node.val <= 100
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
func zigzagLevelOrder(root *TreeNode) [][]int {
    if root == nil {
        return [][]int{}
    }
    res := make([][]int, 0)
    stack := make([] *TreeNode, 0)
    stack = append(stack, root)
    flag := 0
    for len(stack) > 0 {
        length := len(stack)
        tmp := make([]int, 0)
        for i := 0; i < length; i++ {
            node := stack[0]
            stack = stack[1:]
            if flag % 2 == 0 {
                tmp = append(tmp, node.Val)
            } else {
                tmp = append([]int{node.Val}, tmp...)
            }
            if node.Left != nil {
                stack = append(stack, node.Left)
            }
            if node.Right != nil {
                stack = append(stack, node.Right)
            }
        }
        res = append(res, tmp)
        flag++
    }
    return res
}
```