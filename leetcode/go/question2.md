```
给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

 

示例 1：


输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
示例 2：

输入：l1 = [0], l2 = [0]
输出：[0]
示例 3：

输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
 

提示：

每个链表中的节点数在范围 [1, 100] 内
0 <= Node.val <= 9
题目数据保证列表表示的数字不含前导零
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
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    ret_head := &ListNode{}
    ret_tail := ret_head
    jin := 0
    for l1 != nil && l2 != nil {
        tmp := l1.Val + l2.Val + jin
        value := 0
        if tmp >= 10 {
            value = tmp - 10
            jin = 1
        } else {
            value = tmp
            jin = 0
        }
        new_node := &ListNode{}
        new_node.Val = value
        ret_tail.Next = new_node
        ret_tail = new_node
        l1 = l1.Next
        l2 = l2.Next
    }

    for l1 != nil {
        tmp := l1.Val + jin
        value := 0
        if tmp >= 10 {
            value = tmp - 10
            jin = 1
        } else {
            value = tmp
            jin = 0
        }
        new_node := &ListNode{}
        new_node.Val = value
        ret_tail.Next = new_node
        ret_tail = new_node
        l1 = l1.Next
    }

    for l2 != nil {
        tmp := l2.Val + jin
        value := 0
        if tmp >= 10 {
            value = tmp - 10
            jin = 1
        } else {
            value = tmp
            jin = 0
        }
        new_node := &ListNode{}
        new_node.Val = value
        ret_tail.Next = new_node
        ret_tail = new_node
        l2 = l2.Next
    }

    if jin == 1 {
        new_node := &ListNode{}
        new_node.Val = 1
        ret_tail.Next = new_node
        ret_tail = new_node
    }

    ret_tail.Next = nil
    return ret_head.Next
}
```