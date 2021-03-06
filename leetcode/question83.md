```
给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

示例 1:

输入: 1->1->2
输出: 1->2
示例 2:

输入: 1->1->2->3->3
输出: 1->2->3
```

```
class ListNode {
    public $val = 0;

    public $next = null;

    function __construct($val = 0, $next = null) {
        $this->val = $val;
        $this->next = $next;
    }
}
class Solution {
    /**
     * @param ListNode $head
     *
     * @return ListNode
     */
    function deleteDuplicates($head) {
        $ret_head = $ret_tail = new ListNode();
        while ($head != null) {
            if ($head->next == null) {
                $node = new ListNode($head->val);
                $ret_tail->next = $node;
                $ret_tail = $node;
                break;
            }
            if ($head->val == $head->next->val) {
                $head->next = $head->next->next;
            } else {
                $node = new ListNode($head->val);
                $ret_tail->next = $node;
                $ret_tail = $node;
                $head = $head->next;

            }
        }
        $ret_tail->next = null;

        return $ret_head->next;
    }

    function buildTail($arr) {
        $head = $tail = new ListNode();
        foreach ($arr as $value) {
            $node = new ListNode($value);
            $tail->next = $node;
            $tail = $node;
        }
        $tail->next = null;

        return $head->next;
    }
}
```