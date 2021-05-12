```
给你一个链表的头节点 head 和一个特定值 x ，请你对链表进行分隔，使得所有 小于 x 的节点都出现在 大于或等于 x 的节点之前。
你应当保留两个分区中每个节点的初始相对位置。

示例 1：
输入：head = [1,4,3,2,5,2], x = 3
输出：[1,2,2,4,3,5]

示例 2：
输入：head = [2,1], x = 2
输出：[1,2]
 
提示：
链表中节点的数目在范围 [0, 200] 内
-100 <= Node.val <= 100
-200 <= x <= 200
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
     * @param Integer $x
     * @return ListNode
     */
    function partition($head, $x) {
        $small_head = $small_tail = new ListNode();
        $big_head = $big_tail = new ListNode();
        while ($head != null) {
            $val = $head->val;
            if ($val < $x) {
                $small_node = new ListNode($val);
                $small_tail->next = $small_node;
                $small_tail = $small_node;
            } else {
                $big_node = new ListNode($val);
                $big_tail->next = $big_node;
                $big_tail = $big_node;
            }
            $head = $head->next;
        }
        $small_tail->next = $big_head->next;
        $big_tail->next = null;
        
        return $small_head->next;
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