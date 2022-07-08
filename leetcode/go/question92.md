```
给你单链表的头指针 head 和两个整数 left 和 right ，其中 left <= right 。请你反转从位置 left 到位置 right 的链表节点，返回 反转后的链表 。
 

示例 1：


输入：head = [1,2,3,4,5], left = 2, right = 4
输出：[1,4,3,2,5]
示例 2：

输入：head = [5], left = 1, right = 1
输出：[5]
 

提示：

链表中节点数目为 n
1 <= n <= 500
-500 <= Node.val <= 500
1 <= left <= right <= n
 

进阶： 你可以使用一趟扫描完成反转吗？
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
func reverseBetween(head *ListNode, left int, right int) *ListNode {
    dummy := &ListNode{}
    dummy.Next = head
    start := dummy

    for i := 0; i < left - 1; i++ {
        start = start.Next
    }

    end := start
    for j := 0; j < right - left + 1; j++ {
        end = end.Next
    }

    start_next := start.Next
    end_next := end.Next

    start.Next = nil
    end.Next = nil

    reverse(start_next)

    start.Next = end
    start_next.Next = end_next

    return dummy.Next
}

func reverse(head *ListNode) *ListNode {
    pre := &ListNode{}
    cur := head
    for cur != nil {
        next := cur.Next
        cur.Next = pre
        pre = cur
        cur = next
    }
    return pre
}
```