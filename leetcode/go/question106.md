```
给定两个整数数组 inorder 和 postorder ，其中 inorder 是二叉树的中序遍历， postorder 是同一棵树的后序遍历，请你构造并返回这颗 二叉树 。

 

示例 1:


输入：inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
输出：[3,9,20,null,null,15,7]
示例 2:

输入：inorder = [-1], postorder = [-1]
输出：[-1]
 

提示:

1 <= inorder.length <= 3000
postorder.length == inorder.length
-3000 <= inorder[i], postorder[i] <= 3000
inorder 和 postorder 都由 不同 的值组成
postorder 中每一个值都在 inorder 中
inorder 保证是树的中序遍历
postorder 保证是树的后序遍历
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
func buildTree(inorder []int, postorder []int) *TreeNode {
    if len(inorder) == 0 {
        return nil
    }
    root_val := postorder[len(postorder) - 1]
    root := &TreeNode{}
    root.Val = root_val
    find := 0
    for i := 0; i < len(inorder); i++ {
        if inorder[i] == root_val {
            find = i
            break
        }
    }
    inorder_left := inorder[:find]
    inorder_right := inorder[find + 1:]
    postorder_left := postorder[:find]
    postorder_right := postorder[find:len(postorder) - 1]
    root.Left = buildTree(inorder_left, postorder_left)
    root.Right = buildTree(inorder_right, postorder_right)
    return root
}
```