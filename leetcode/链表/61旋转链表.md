```
给你一个链表的头节点 head ，旋转链表，将链表每个节点向右移动 k 个位置。

 

示例 1：


输入：head = [1,2,3,4,5], k = 2
输出：[4,5,1,2,3]
示例 2：


输入：head = [0,1,2], k = 4
输出：[2,0,1]
 

提示：

链表中节点的数目在范围 [0, 500] 内
-100 <= Node.val <= 100
0 <= k <= 2 * 109
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
func rotateRight(head *ListNode, k int) *ListNode {
    if head == nil {
        return head
    }
    head_bak := head
    length := 1
    for head_bak.Next != nil {
        head_bak = head_bak.Next
        length++
    }
    head_bak.Next = head

    move := length - k % length

    for move > 1 {
        head = head.Next
        move--
    }

    new_head := head.Next
    head.Next = nil
    return new_head
}
```