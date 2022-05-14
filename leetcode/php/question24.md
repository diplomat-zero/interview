```
给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。
你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

示例 1：
输入：head = [1,2,3,4]
输出：[2,1,4,3]

示例 2：
输入：head = []
输出：[]

示例 3：
输入：head = [1]
输出：[1]
 
提示：
链表中节点的数目在范围 [0, 100] 内
0 <= Node.val <= 100
 
进阶：你能在不修改链表节点值的情况下解决这个问题吗?（也就是说，仅修改节点本身。）
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
    function swapPairs($head) {
        if ($head == null || $head->next == null) {
            return $head;
        }
        $one = $head;
        $two = $head->next;
        $three = $two->next;

        $one->next = $this->swapPairs($three);
        $two->next = $one;
        return $two;
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
     *
     * @return ListNode
     */
    function swapPairs($head) {
        $ret_head = $ret_tail = new ListNode();
        while ($head != null) {
            $next = $head->next;

            if ($next != null) {
                $node_next_next = new ListNode($next->val);
                $ret_tail->next = $node_next_next;
                $ret_tail = $node_next_next;
            }

            $node_next = new ListNode($head->val);
            $ret_tail->next = $node_next;
            $ret_tail = $node_next;

            $head = $head->next->next;
        }

        $ret_tail->next = null;
        return $ret_head->next;
    }

    function buildTail($arr) {
        $head = $tail = new ListNode();
        foreach ($arr as $value) {
            $node =  new ListNode($value);
            $tail->next = $node;
            $tail = $node;
        }
        $tail->next = null;

        return $head->next;
    }
}
```