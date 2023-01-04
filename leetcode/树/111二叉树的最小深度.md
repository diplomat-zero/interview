```
给定一个二叉树，找出其最小深度。
最小深度是从根节点到最近叶子节点的最短路径上的节点数量。
说明：叶子节点是指没有子节点的节点。

示例 1：
输入：root = [3,9,20,null,null,15,7]
输出：2

示例 2：
输入：root = [2,null,3,null,4,null,5,null,6]
输出：5
 
提示：
树中节点数的范围在 [0, 105] 内
-1000 <= Node.val <= 1000
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
func minDepth(root *TreeNode) int {
    if root == nil {
        return 0
    }

    step := 1
    queue := make([]*TreeNode, 0);
    queue = append(queue, root);
    for l := len(queue); l > 0; {
        length := len(queue)
        for i := 0; i < length; i++ {
            cur := queue[0]
            if cur.Left == nil && cur.Right == nil {
                return step
            }
            if cur.Left != nil {
                queue = append(queue, cur.Left)
            }
            if cur.Right != nil {
                queue = append(queue, cur.Right)
            }
            queue = queue[1:]
        }
        step++
    }

    return step
}
```