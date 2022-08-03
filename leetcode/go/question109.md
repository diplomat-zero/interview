```
给定一个单链表的头节点  head ，其中的元素 按升序排序 ，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差不超过 1。

 

示例 1:



输入: head = [-10,-3,0,5,9]
输出: [0,-3,9,-10,null,5]
解释: 一个可能的答案是[0，-3,9，-10,null,5]，它表示所示的高度平衡的二叉搜索树。
示例 2:

输入: head = []
输出: []
 

提示:

head 中的节点数在[0, 2 * 104] 范围内
-105 <= Node.val <= 105
```

```

```

```
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sortedListToBST(head *ListNode) *TreeNode {
    return buildTree(head, nil)
}

func buildTree(head *ListNode, tail *ListNode) *TreeNode {
    if head == tail {
        return nil
    }
    mid := getMedian(head, tail)
    root := &TreeNode{mid.Val, nil, nil}
    root.Left = buildTree(head, mid)
    root.Right = buildTree(mid.Next, tail)
    return root
}

func getMedian(left, right *ListNode) *ListNode {
    fast, slow := left, left
    for fast != right && fast.Next != right {
        fast = fast.Next.Next
        slow = slow.Next
    }
    return slow
}
```