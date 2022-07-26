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
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode start = dummy;
        
        for (int i = 0; i < left - 1; i++) {
            start = start.next;
        }

        ListNode end = start;
        for (int j = 0; j < right - left + 1; j++) {
            end = end.next;
        }

        ListNode start_next = start.next;
        ListNode end_next = end.next;

        start.next = null;
        end.next = null;

        reverse(start_next);

        start.next = end;
        start_next.next = end_next;
        return dummy.next;
    }

    public ListNode reverse(ListNode start) {
        ListNode pre;
        pre = null;
        ListNode cur = start;
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