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
     * @return Boolean
     */
    function isPalindrome($head) {
        $slow = $fast = $head;
        while ($fast != null && $fast->next != null) {
            $slow = $slow->next;
            $fast = $fast->next->next;
        }
        $slow = $this->reserve($slow);
        while ($head != null && $slow != null) {
            if ($head->val != $slow->val) {
                return false;
            }
            $head = $head->next;
            $slow = $slow->next;
        }
        return true;
    }

    function reserve($head) {
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