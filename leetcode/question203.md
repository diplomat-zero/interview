```
给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点 。

示例 1：
输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]

示例 2：
输入：head = [], val = 1
输出：[]

示例 3：
输入：head = [7,7,7,7], val = 7
输出：[]
 
提示：
列表中的节点在范围 [0, 104] 内
1 <= Node.val <= 50
0 <= k <= 50
```

```
<?php
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
     * @param Integer $val
     * @return ListNode
     */
    function removeElements($head, $val) {
        $prev = $head;
        $cur = $head->next;
        while ($cur != null) {
            if ($cur->val == $val) {
                $prev->next = $cur->next;
            } else {
                $prev = $cur;
            }

            $cur = $cur->next;
        }
        return $head->val == $val ? $head->next : $head;
    }

    function buildTail($arr) {
        $head = $tail = new ListNode();
        foreach ($arr as $value) {
            $new_node = new ListNode($value);
            $tail->next = $new_node;
            $tail = $new_node;
        }
        $tail->next = null;
        return $head->next;
    }
}
```