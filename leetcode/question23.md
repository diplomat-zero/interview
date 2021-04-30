```
给你一个链表数组，每个链表都已经按升序排列。
请你将所有链表合并到一个升序链表中，返回合并后的链表。

示例 1：
输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6

示例 2：
输入：lists = []
输出：[]

示例 3：
输入：lists = [[]]
输出：[]
 
提示：

k == lists.length
0 <= k <= 10^4
0 <= lists[i].length <= 500
-10^4 <= lists[i][j] <= 10^4
lists[i] 按 升序 排列
lists[i].length 的总和不超过 10^4
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
     * @param ListNode[] $lists
     * @return ListNode
     */
    function mergeKLists($lists) {
        if (empty($lists)) {
            return [];
        }
        if (count($lists) == 1) {
            return $lists[0];
        }
        $mid = intval(count($lists) / 2);
        $left = self::mergeKLists(array_slice($lists, 0, $mid));
        $right = self::mergeKLists(array_slice($lists, $mid));
        return self::merge($left, $right);
    }

    function merge($head1, $head2) {
        $head = $tail = new ListNode();
        while ($head1 != null && $head2 != null) {
            if ($head1->val > $head2->val) {
                $newNode = new ListNode($head2->val);
                $tail->next = $newNode;
                $tail = $newNode;
                $head2 = $head2->next;
            } else {
                $newNode = new ListNode($head1->val);
                $tail->next = $newNode;
                $tail = $newNode;
                $head1 = $head1->next;
            }
        }
        while ($head1 != null) {
            $newNode = new ListNode($head1->val);
            $tail->next = $newNode;
            $tail = $newNode;
            $head1 = $head1->next;
        }
        while ($head2 != null) {
            $newNode = new ListNode($head2->val);
            $tail->next = $newNode;
            $tail = $newNode;
            $head2 = $head2->next;
        }
        $tail->next = null;
        return $head->next;
    }
}
```