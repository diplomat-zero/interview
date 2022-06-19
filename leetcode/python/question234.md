```
给你一个单链表的头节点 head ，请你判断该链表是否为回文链表。如果是，返回 true ；否则，返回 false 。

 

示例 1：


输入：head = [1,2,2,1]
输出：true
示例 2：


输入：head = [1,2]
输出：false
 

提示：

链表中节点数目在范围[1, 105] 内
0 <= Node.val <= 9
 

进阶：你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？
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
    def isPalindrome(self, head: ListNode) -> bool:
        def reverse(head):
            pre = None
            cur = head
            while cur != None:
                next_node = cur.next
                cur.next = pre
                pre = cur
                cur = next_node
            return pre
        
        fast = slow = head
        while fast != None and fast.next != None:
            slow = slow.next
            fast = fast.next.next
        
        if fast != None:
            slow = slow.next
        
        right = reverse(slow)
        
        left = head
        while right != None:
            if left.val != right.val:
                return False
            left = left.next
            right = right.next
        
        return True
```