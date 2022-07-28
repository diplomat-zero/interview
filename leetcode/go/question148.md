```
给你链表的头结点 head ，请将其按 升序 排列并返回 排序后的链表 。

 

示例 1：


输入：head = [4,2,1,3]
输出：[1,2,3,4]
示例 2：


输入：head = [-1,5,3,4,0]
输出：[-1,0,3,4,5]
示例 3：

输入：head = []
输出：[]
 

提示：

链表中节点的数目在范围 [0, 5 * 104] 内
-105 <= Node.val <= 105
 

进阶：你可以在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序吗？
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
func sortList(head *ListNode) *ListNode {
    return mergeList(head, nil)
}

func mergeList(head *ListNode, tail *ListNode) *ListNode {
    if head == nil {
        return head
    }
    if head.Next == tail {
        head.Next = nil
        return head
    }

    slow, fast := head, head
    for fast != tail {
        slow = slow.Next
        fast = fast.Next
        if fast != tail {
            fast = fast.Next
        }
    }

    mid := slow
    head1 := mergeList(head, mid)
    head2 := mergeList(mid, tail)
    return merge(head1, head2)
}

func merge(head1 *ListNode, head2 *ListNode) *ListNode {
    ret_tail := &ListNode{}
    ret_tail.Val = 0
    ret_head := ret_tail
    for head1 != nil && head2 != nil {
        if head1.Val > head2.Val {
            ret_tail.Next = head2
            head2 = head2.Next
        } else {
            ret_tail.Next = head1
            head1 = head1.Next
        }
        ret_tail = ret_tail.Next
    }

    if head1 != nil {
        ret_tail.Next = head1;
    }

    if head2 != nil {
        ret_tail.Next = head2;
    }

    return ret_head.Next;
}
```