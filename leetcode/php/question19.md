```
给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

进阶：你能尝试使用一趟扫描实现吗？

示例 1：
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]

示例 2：
输入：head = [1], n = 1
输出：[]

示例 3：
输入：head = [1,2], n = 1
输出：[1]
 
提示：

链表中结点的数目为 sz
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz
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
     * @param Integer  $n
     *
     * @return ListNode
     */
    function removeNthFromEnd($head, $n) {
        $total = 0;
        $tmp = $head;
        while ($tmp != null) {
            $total++;
            $tmp = $tmp->next;
        }

        $i = 1;
        $target = $total + 1 - $n;
        $new_head = $new_tail = new ListNode();
        while ($head != null) {
            if ($target == $i) {
                $i++;
                $head = $head->next;
                continue;
            }
            $node = new ListNode($head->val);
            $new_tail->next = $node;
            $new_tail = $node;
            $head = $head->next;
            $i++;
        }
        $new_tail->next = null;

        return $new_head->next;
    }

    function buildHead($arr) {
        $head = new ListNode();
        foreach ($arr as $value) {
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