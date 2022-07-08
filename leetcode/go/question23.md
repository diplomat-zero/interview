```
给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

 

示例 1：

输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6
示例 2：

输入：lists = []
输出：[]
示例 3：

输入：lists = [[]]
输出：[]
 

提示：

k == lists.length
0 <= k <= 10^4
0 <= lists[i].length <= 500
-10^4 <= lists[i][j] <= 10^4
lists[i] 按 升序 排列
lists[i].length 的总和不超过 10^4
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
func mergeKLists(lists []*ListNode) *ListNode {
    if len(lists) == 0 {
        return nil
    }
    if len(lists) == 1 {
        return lists[0]
    }

    mid := len(lists) / 2
    list1 := mergeKLists(lists[:mid])
    list2 := mergeKLists(lists[mid:])
    return merge(list1, list2)
}

func merge(list1 *ListNode, list2 *ListNode) *ListNode {
    ret_tail := &ListNode{}
    ret_head := ret_tail
    for list1 != nil && list2 != nil {
        if list1.Val > list2.Val {
            ret_tail.Next = list2
            list2 = list2.Next
        } else {
            ret_tail.Next = list1
            list1 = list1.Next
        }
        ret_tail = ret_tail.Next
    }

    if list1 != nil {
        ret_tail.Next = list1
    }

    if list2 != nil {
        ret_tail.Next = list2
    }

    return ret_head.Next
}
```

```
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func mergeKLists(lists []*ListNode) *ListNode {
    if len(lists) == 0 {
        return nil
    }
    if len(lists) == 1 {
        return lists[0]
    }

    mid := len(lists) / 2
    list1 := mergeKLists(lists[:mid])
    list2 := mergeKLists(lists[mid:])
    return merge(list1, list2)
}

func merge(list1 *ListNode, list2 *ListNode) *ListNode {
    ret_tail := &ListNode{}
    ret_head := ret_tail
    for list1 != nil && list2 != nil {
        new_val := 0
        if list1.Val > list2.Val {
            new_val = list2.Val
            list2 = list2.Next
        } else {
            new_val = list1.Val
            list1 = list1.Next
        }
        new_node := &ListNode{}
        new_node.Val = new_val
        ret_tail.Next = new_node
        ret_tail = new_node
    }

    for list1 != nil {
        new_node := &ListNode{}
        new_node.Val = list1.Val
        ret_tail.Next = new_node
        ret_tail = new_node
        list1 = list1.Next
    }

    for list2 != nil {
        new_node := &ListNode{}
        new_node.Val = list2.Val
        ret_tail.Next = new_node
        ret_tail = new_node
        list2 = list2.Next
    }

    ret_tail.Next = nil
    return ret_head.Next
}
```