```
输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

示例1：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
限制：

0 <= 链表长度 <= 1000
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
func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
    ret_head := &ListNode{}
    ret_tail := ret_head
    for l1 != nil && l2 != nil {
        if l1.Val > l2.Val {
            ret_tail.Next = l2
            l2 = l2.Next
        } else {
            ret_tail.Next = l1
            l1 = l1.Next
        }
        ret_tail = ret_tail.Next
    }
    if l1 != nil {
        ret_tail.Next = l1
    }
    if l2 != nil {
        ret_tail.Next = l2
    }
    return ret_head.Next
}
```