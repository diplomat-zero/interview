```
给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

示例 1:

输入: 1->2->3->3->4->4->5
输出: 1->2->5
示例 2:

输入: 1->1->1->2->3
输出: 2->3
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
    function deleteDuplicates($head) {
        $ret_head = $ret_tail = new ListNode(0);
        while ($head != null) {
            if ($head->val == $head->next->val) {
                $tmp = $head->val;
                while ($head != null && $head->val == $tmp) {
                    $head = $head->next;
                }
            } else {
                $new_node = new ListNode($head->val);
                $ret_tail->next = $new_node;
                $ret_tail = $new_node;
                $head = $head->next;
            }
        }

        $ret_tail->next = null;
        return $ret_head->next;
    }
}
```

```
class ListNode {
    public $val;

    public $next;

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
        $tmp = $head;
        $del = [];
        while ($tmp != null) {
            $tmp_value = $tmp->val;
            $tmp_next_value = $tmp->next->val;
            if ($tmp_value == $tmp_next_value) {
                !isset($del[$tmp_value]) && $del[$tmp_value] = $tmp_value;
            }
            $tmp = $tmp->next;
        }

        if (empty($del)) {
            return $head;
        }

        $ret_head = $ret_tail = new ListNode();
        while ($head != null) {
            if (isset($del[$head->val])) {
                $head = $head->next;
                continue;
            }
            $node = new ListNode($head->val);
            $ret_tail->next = $node;
            $ret_tail = $node;
            $head = $head->next;
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