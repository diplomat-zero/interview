```
给定一个非空二叉树的根节点 root , 以数组的形式返回每一层节点的平均值。与实际答案相差 10-5 以内的答案可以被接受。

 

示例 1：



输入：root = [3,9,20,null,null,15,7]
输出：[3.00000,14.50000,11.00000]
解释：第 0 层的平均值为 3,第 1 层的平均值为 14.5,第 2 层的平均值为 11 。
因此返回 [3, 14.5, 11] 。
示例 2:



输入：root = [3,9,20,15,7]
输出：[3.00000,14.50000,11.00000]
 

提示：

树中节点数量在 [1, 104] 范围内
-231 <= Node.val <= 231 - 1
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
func averageOfLevels(root *TreeNode) []float64 {
    stack := make([]*TreeNode, 0)
    stack = append(stack, root)
    res := make([]float64, 0)
    for len(stack) > 0 {
        length := len(stack)
        sum := 0
        count := 0
        for i := 0; i < length; i++ {
            node := stack[0]
            stack = stack[1:]
            if node.Left != nil {
                stack = append(stack, node.Left)
            }
            if node.Right != nil {
                stack = append(stack, node.Right)
            }
            sum += node.Val
            count++
        }
        res = append(res, float64(sum) / float64(count))
    }
    return res
}
```