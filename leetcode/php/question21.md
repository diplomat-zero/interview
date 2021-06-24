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
     * @param ListNode $l1
     * @param ListNode $l2
     *
     * @return ListNode
     */
    function mergeTwoLists($l1, $l2) {
        $ret_head = $ret_tail = new ListNode();
        while ($l1 != null && $l2 != null) {
            if ($l1->val > $l2->val) {
                $node = new ListNode($l2->val);
                $l2 = $l2->next;
            } else {
                $node = new ListNode($l1->val);
                $l1 = $l1->next;
            }
            $ret_tail->next = $node;
            $ret_tail = $node;
        }

        while ($l1 != null) {
            $node = new ListNode($l1->val);
            $ret_tail->next = $node;
            $ret_tail = $node;
            $l1 = $l1->next;
        }

        while ($l2 != null) {
            $node = new ListNode($l2->val);
            $ret_tail->next = $node;
            $ret_tail = $node;
            $l2 = $l2->next;
        }

        $ret_tail->next = null;
        return $ret_head->next;
    }

    function buildHead($arr) {
        $head = new ListNode();
        foreach ($head as $value) {
            $node = new ListNode($value);
            $node->next = $head->next;
            $head->next = $node;
        }

        return $head->next;
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