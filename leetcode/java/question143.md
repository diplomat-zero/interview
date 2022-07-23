```
给定一个单链表 L 的头节点 head ，单链表 L 表示为：

L0 → L1 → … → Ln - 1 → Ln
请将其重新排列后变为：

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

 

示例 1：



输入：head = [1,2,3,4]
输出：[1,4,2,3]
示例 2：



输入：head = [1,2,3,4,5]
输出：[1,5,2,4,3]
 

提示：

链表的长度范围为 [1, 5 * 104]
1 <= node.val <= 1000
```

```

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
    public void reorderList(ListNode head) {
        ListNode slow,fast;
        slow = head;
        fast = head;
        while (fast != null && fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        ListNode right = reverse(slow);

        ListNode left = head;
        while (left != null) {
            ListNode left_next = left.next;
            ListNode right_next = right.next;

            left.next = right;
            right.next = left_next;

            left = left_next;
            right = right_next;
        }
    }

    public ListNode reverse(ListNode head) {
        ListNode pre;
        pre = null;
        ListNode cur = head;
        while (cur != null) {
            ListNode next_node = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next_node;
        }
        return pre;
    }
}
```