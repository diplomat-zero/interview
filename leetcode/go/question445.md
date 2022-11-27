```
给你两个 非空 链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

 

示例1：



输入：l1 = [7,2,4,3], l2 = [5,6,4]
输出：[7,8,0,7]
示例2：

输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[8,0,7]
示例3：

输入：l1 = [0], l2 = [0]
输出：[0]
 

提示：

链表的长度范围为 [1, 100]
0 <= node.val <= 9
输入数据保证链表代表的数字无前导 0
 

进阶：如果输入链表不能翻转该如何解决？
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
    l1_bak := reverse(l1)
    l2_bak := reverse(l2)
    ret_head := &ListNode{}
    ret_tail := ret_head
    jin := 0
    for l1_bak != nil || l2_bak != nil || jin != 0 {
        l1_bak_val := 0
        if l1_bak != nil {
            l1_bak_val = l1_bak.Val
            l1_bak = l1_bak.Next
        }
        l2_bak_val := 0
        if l2_bak != nil {
            l2_bak_val = l2_bak.Val
            l2_bak = l2_bak.Next
        }
        value := 0
        tmp := l1_bak_val + l2_bak_val + jin
        if tmp >= 10 {
            value = tmp - 10
            jin = 1
        } else {
            value = tmp
            jin = 0
        }
        node := &ListNode{Val: value}
        ret_tail.Next = node
        ret_tail = node
    }
    return reverse(ret_head.Next)
}

func reverse(head *ListNode) *ListNode {
    var pre *ListNode
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