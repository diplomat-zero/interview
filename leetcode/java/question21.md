```
将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例 1：
输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]

示例 2：
输入：l1 = [], l2 = []
输出：[]

示例 3：
输入：l1 = [], l2 = [0]
输出：[0]
 
提示：

两个链表的节点数目范围是 [0, 50]
-100 <= Node.val <= 100
l1 和 l2 均按 非递减顺序 排列
```

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode tail = new ListNode();
        ListNode head = tail;
        while(l1 != null && l2 != null) {
            ListNode new_node = new ListNode();
            if (l1.val > l2.val) {
                new_node.val = l2.val;
                l2 = l2.next;
            } else {
                new_node.val = l1.val;
                l1 = l1.next;
            }
            tail.next = new_node;
            tail = new_node;
        }

        while (l1 != null) {
            ListNode new_node = new ListNode();
            new_node.val = l1.val;
            tail.next = new_node;
            tail = new_node;
            l1 = l1.next;
        }

        while (l2 != null) {
            ListNode new_node = new ListNode();
            new_node.val = l2.val;
            tail.next = new_node;
            tail = new_node;
            l2 = l2.next;
        }

        return head.next;
    }
}
```