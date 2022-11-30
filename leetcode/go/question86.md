```
给你一个链表的头节点 head 和一个特定值 x ，请你对链表进行分隔，使得所有 小于 x 的节点都出现在 大于或等于 x 的节点之前。

你应当 保留 两个分区中每个节点的初始相对位置。

 

示例 1：


输入：head = [1,4,3,2,5,2], x = 3
输出：[1,2,2,4,3,5]
示例 2：

输入：head = [2,1], x = 2
输出：[1,2]
 

提示：

链表中节点的数目在范围 [0, 200] 内
-100 <= Node.val <= 100
-200 <= x <= 200
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
func partition(head *ListNode, x int) *ListNode {
    small_head := &ListNode{}
    small_tail := small_head
    big_head := &ListNode{}
    big_tail := big_head
    for head != nil {
        node := &ListNode{Val: head.Val}
        if head.Val < x {
            small_tail.Next = node
            small_tail = node
        } else {
            big_tail.Next = node
            big_tail = node
        }
        head = head.Next
    }
    small_tail.Next = nil
    big_tail.Next = nil
    small_tail.Next = big_head.Next
    return small_head.Next
}
```