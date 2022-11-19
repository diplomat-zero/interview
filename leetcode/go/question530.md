```
给你一个二叉搜索树的根节点 root ，返回 树中任意两不同节点值之间的最小差值 。

差值是一个正数，其数值等于两值之差的绝对值。

 

示例 1：


输入：root = [4,2,6,1,3]
输出：1
示例 2：


输入：root = [1,0,48,null,null,12,49]
输出：1
 

提示：

树中节点的数目范围是 [2, 104]
0 <= Node.val <= 105
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
func getMinimumDifference(root *TreeNode) int {
    if root == nil {
        return 0
    }
    last = math.MinInt64
    res = math.MaxInt64
    inorder(root)
    return res
}

var last int
var res int

func inorder(root *TreeNode) {
    if root == nil {
        return
    }
    inorder(root.Left)
    if math.Abs(float64(root.Val) - float64(last)) < float64(res) {
        res = root.Val - last
    }
    last = root.Val
    inorder(root.Right)
}
```