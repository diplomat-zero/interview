```
给定二叉树的根节点 root，找出存在于 不同 节点 A 和 B 之间的最大值 V，其中 V = |A.val - B.val|，且 A 是 B 的祖先。

（如果 A 的任何子节点之一为 B，或者 A 的任何子节点是 B 的祖先，那么我们认为 A 是 B 的祖先）

 

示例 1：



输入：root = [8,3,10,1,6,null,14,null,null,4,7,13]
输出：7
解释： 
我们有大量的节点与其祖先的差值，其中一些如下：
|8 - 3| = 5
|3 - 7| = 4
|8 - 1| = 7
|10 - 13| = 3
在所有可能的差值中，最大值 7 由 |8 - 1| = 7 得出。
示例 2：


输入：root = [1,null,2,null,0,3]
输出：3
 

提示：

树中的节点数在 2 到 5000 之间。
0 <= Node.val <= 105
```

```
就一个节点来说所谓最大差值，就是祖先的最大值或者最小值和自己的val的差值。 只需要知道所有祖先可能的最大值和最小值，在遍历时携带传递即可。
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
func maxAncestorDiff(root *TreeNode) int {
    result := 0
    var helper func(*TreeNode, int, int)
    helper = func(root *TreeNode, maxNum int, minNum int) {
        if root == nil {
            return 
        }
        result = max(result,max(int(math.Abs(float64(maxNum - root.Val))),int(math.Abs(float64(minNum - root.Val)))))
        maxNum = max(maxNum, root.Val)
        minNum = min(minNum, root.Val)
        helper(root.Left, maxNum, minNum)
        helper(root.Right, maxNum, minNum)
    }
    helper(root, root.Val, root.Val)
    return result
}

func max(a,b int) int {
    if a > b {
        return a
    }
    return b
}

func min(a,b int) int {
    if a < b {
        return a
    }
    return b
}
```