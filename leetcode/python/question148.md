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
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        def sort(head, tail):
            if head is None:
                return head
            if head.next == tail:
                head.next = None
                return head
            slow = fast = head
            while fast != tail:
                slow = slow.next
                fast = fast.next
                if fast != tail:
                    fast = fast.next
            mid = slow
            res1 = sort(head, mid)
            res2 = sort(mid, tail)
            return merge(res1, res2)
        
        def merge(list1, list2):
            ret_head = ret_tail = ListNode()
            while list1 != None and list2 != None:
                if list1.val > list2.val:
                    new_value = list2.val
                    list2 = list2.next
                else:
                    new_value = list1.val
                    list1 = list1.next
                new_node = ListNode(new_value)
                ret_tail.next = new_node
                ret_tail = new_node
            
            while list1 != None:
                new_node = ListNode(list1.val)
                ret_tail.next = new_node
                ret_tail = new_node
                list1 = list1.next
            
            while list2 != None:
                new_node = ListNode(list2.val)
                ret_tail.next = new_node
                ret_tail = new_node
                list2 = list2.next
            
            ret_tail.next = None
            return ret_head.next

        return sort(head, None)
```