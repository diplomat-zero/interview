```
给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。
 
示例 1：
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]

示例 2：
输入：head = [1,2]
输出：[2,1]

示例 3：
输入：head = []
输出：[]
 
提示：
链表中节点的数目范围是 [0, 5000]
-5000 <= Node.val <= 5000
进阶：链表可以选用迭代或递归方式完成反转。你能否用两种方法解决这道题？
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
     * @return ListNode
     */
    function reverseList($head) {
        $result = new ListNode();
        while ($head != null) {
            $new_node = new ListNode($head->val);
            $new_node->next = $result->next;
            $result->next = $new_node;
            $head = $head->next;
        }
        return $result->next;
    }

    function buildHead($arr) {
        $head = new ListNode();
        foreach ($arr as $value) {
            $newNode = new ListNode($value);
            $newNode->next = $head->next;
            $head->next = $newNode;
        }
        return $head->next;
    }

    function buildTail($arr) {
        $head = $tail = new ListNode();
        foreach ($arr as $val) {
            $new_node = new ListNode($val);
            $tail->next = $new_node;
            $tail = $new_node;
        }
        $tail->next = null;
        return $head->next;
    }
}
```