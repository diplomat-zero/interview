```
给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

示例 1:

输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
示例 2:

输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
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
     * @param Integer $k
     * @return ListNode
     */
    function rotateRight($head, $k) {
        if ($head == null) {
            return $head;
        }
        $head_bak = $head;
        $len = 1;
        while ($head_bak->next != null) {
            $head_bak = $head_bak->next;
        $len++;
        }
        $tail = $head_bak;

        $tail->next = $head;
        $move = $len - $k % $len;
        while ($move > 1) {
            $head = $head->next;
            $move--;
        }
        $ret = $head->next;
        $head->next = null;
        return $ret;
    }
}
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
     * @param Integer  $k
     *
     * @return ListNode
     */
    function rotateRight($head, $k) {
        if ($k == 0 || $head == null) {
            return $head;
        }
        $head_head = $head;
        $tmp = $head;
        $total = 0;
        while ($tmp != null) {
            $total++;
            $tmp = $tmp->next;
        }

        $move = $k % $total;
        if ($move == 0) {
            return $head;
        }

        $ret_head = $ret_tail = new ListNode();
        $i = 0;
        $n = $total - $move + 1;
        while ($head != null) {
            $i++;
            if ($i < $n) {
                $head = $head->next;
                continue;
            }
            $node = new ListNode($head->val);
            $ret_tail->next = $node;
            $ret_tail = $node;
            $head = $head->next;
        }

        $j = 0;
        while ($j < $total - $move && $head_head != null) {
            $node = new ListNode($head_head->val);
            $ret_tail->next = $node;
            $ret_tail = $node;
            $head_head = $head_head->next;
            $j++;
        }

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