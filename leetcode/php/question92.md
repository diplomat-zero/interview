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
     * @param Integer $left
     * @param Integer $right
     * @return ListNode
     */
    function reverseBetween($head, $left, $right) {
        $result = new ListNode(0);
        $result->next = $head;
        $pre = $result;

        for ($i = 0; $i < $left - 1; $i++) {
            $pre = $pre->next;
        }

        $end = $pre;

        for ($j = 0; $j < $right - $left + 1; $j++) {
            $end = $end->next;
        }

        $middle = $pre->next;
        $cur = $end->next;

        $pre->next = null;
        $end->next = null;

        $this->reverse($middle);

        $pre->next = $end;
        $middle->next = $cur;

        return $result->next;
    }

    function reverse($head)
    {
        $pre = null;
        $cur = $head;
        while ($cur != null) {
            $next = $cur->next;
            $cur->next = $pre;
            $pre = $cur;
            $cur = $next;
        }
        return $cur;
    }
}
```