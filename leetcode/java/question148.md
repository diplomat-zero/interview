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
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode sortList(ListNode head) {
        return mergeSort(head, null);
    }

    public ListNode mergeSort(ListNode head, ListNode tail) {
        if (head == null) {
            return head;
        }
        if (head.next == tail) {
            head.next = null;
            return head;
        }

        ListNode slow,fast;
        slow = fast = head;
        while (fast != tail) {
            slow = slow.next;
            fast = fast.next;
            if (fast != tail) {
                fast = fast.next;
            }
        }

        ListNode mid = slow;

        ListNode head1 = mergeSort(head, mid);
        ListNode head2 =  mergeSort(mid, tail);
        return merge(head1, head2);
    }

    public ListNode merge(ListNode head1, ListNode head2) {
        ListNode ret_head = new ListNode(0);
        ListNode ret_tail = ret_head;
        while (head1 != null && head2 != null) {
            if (head1.val > head2.val) {
                ret_tail.next = head2;
                head2 = head2.next;
            } else {
                ret_tail.next = head1;
                head1 = head1.next;
            }
            ret_tail = ret_tail.next;
        }
        if (head1 != null) {
            ret_tail.next = head1;
        }
        if (head2 != null) {
            ret_tail.next = head2;
        }
        return ret_head.next;
    }
}
```