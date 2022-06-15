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
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        stack1 = []
        stack2 = []
        res = []
        while l1 != None:
            stack1.append(l1)
            l1 = l1.next
        while l2 != None:
            stack2.append(l2)
            l2 = l2.next
        
        jin = 0
        while len(stack1) != 0 and len(stack2) != 0:
            num1 = stack1.pop()
            num2 = stack2.pop()
            tmp = num1.val + num2.val + jin
            if tmp >= 10:
                value = tmp - 10
                jin = 1
            else:
                value = tmp
                jin = 0
            res.append(value)
        
        while len(stack1) != 0:
            num1 = stack1.pop()
            tmp = num1.val + jin
            if tmp >= 10:
                value = tmp - 10
                jin = 1
            else:
                value = tmp
                jin = 0
            
            res.append(value)

        while len(stack2) != 0:
            num2 = stack2.pop()
            tmp = num2.val + jin
            if tmp >= 10:
                value = tmp - 10
                jin = 1
            else:
                value = tmp
                jin = 0
            
            res.append(value)
        
        if jin == 1:
            res.append(1)
        
        ret_head = ret_tail = ListNode(0)
        while len(res) != 0:
            new_node = ListNode(res.pop())
            ret_tail.next = new_node
            ret_tail = new_node
        ret_tail.next = None
        return ret_head.next
```