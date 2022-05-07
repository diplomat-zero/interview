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
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val = 0, $next = null) {
 *         $this->val = $val;
 *         $this->next = $next;
 *     }
 * }
 */
class Solution {

    /**
     * @param ListNode $head
     * @return ListNode
     */
    function sortList($head) {
        return $this->sort1($head, null);
    }

    function sort1($head, $tail) {
        if ($head == null) {
            return $head;
        }

        if ($head->next == $tail) {
            $head->next = null;
            return $head;
        }

        $slow = $fast = $head;
        while ($fast != $tail) {
            $slow = $slow->next;
            $fast = $fast->next;
            if ($fast != $tail) {
                $fast = $fast->next;
            }
        }

        $mid = $slow;
        $list1 = $this->sort1($head, $mid);
        $list2 = $this->sort1($mid, $tail);
        return $this->merge($list1, $list2);
    }

    function merge($head1, $head2) {
        $head = $tail = new ListNode(0);
        while ($head1 != null && $head2 != null) {
            if ($head1->val > $head2->val) {
                $val = $head2->val;
                $head2 = $head2->next;
            } else {
                $val = $head1->val;
                $head1 = $head1->next;
            }
            $new_node = new ListNode($val);
            $tail->next = $new_node;
            $tail = $new_node;
        }
        while ($head1 != null) {
            $new_node = new ListNode($head1->val);
            $tail->next = $new_node;
            $tail = $new_node;
            $head1 = $head1->next;
        }
        while ($head2 != null) {
            $new_node = new ListNode($head2->val);
            $tail->next = $new_node;
            $tail = $new_node;
            $head2 = $head2->next;
        }
        $tail->next = null;
        return $head->next;
    }
}
```