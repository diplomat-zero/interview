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
     * @return NULL
     */
    function reorderList($head) {
        $slow = $head;
        $fast = $head;
        while ($fast != null && $fast->next != null && $fast->next->next != null) {
            $slow = $slow->next;
            $fast = $fast->next->next;
        }

        $hou = $slow;
        $right = $this->reserve($hou);

        $left = $head;

        while ($left != null) {
            $left_next = $left->next;
            $right_next = $right->next;

            $left->next = $right;
            $right->next = $left_next;

            $left = $left_next;
            $right = $right_next;
        }

        return $head;
    }

    function reserve($head)
    {
        $pre = null;
        $cur = $head;
        while ($cur != null) {
            $next = $cur->next;
            $cur->next = $pre;
            $pre = $cur;
            $cur = $next;
        }
        return $pre;
    }
}
```