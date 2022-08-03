```
给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。
本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:
给定的有序链表： [-10, -3, 0, 5, 9],
一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
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
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($val = 0, $left = null, $right = null) {
 *         $this->val = $val;
 *         $this->left = $left;
 *         $this->right = $right;
 *     }
 * }
 */
class Solution {

    /**
     * @param ListNode $head
     * @return TreeNode
     */
    function sortedListToBST($head) {
        return $this->buildTree($head, null);
    }

    function buildTree($head, $tail) {
        if ($head == $tail) {
            return;
        }
        $fast = $slow = $head;
        while ($fast != $tail && $fast->next != $tail) {
            $slow = $slow->next;
            $fast = $fast->next->next;
        }
        $mid = $slow;
        $root = new TreeNode($mid->val);
        $root->left = $this->buildTree($head, $mid);
        $root->right = $this->buildTree($mid->next, $tail);
        return $root;
    }
}
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
  class TreeNode {
      public $val = null;
      public $left = null;
      public $right = null;
      function __construct($val = 0, $left = null, $right = null) {
          $this->val = $val;
          $this->left = $left;
          $this->right = $right;
      }
  }

class Solution {

    /**
     * @param ListNode $head
     * @return TreeNode
     */
    function sortedListToBST($head) {
        if ($head == null) {
            return;
        }
        $qian_head = $qian_tail = new ListNode();
        $slow = $fast = $head;
        while ($fast != null && $fast->next != null) {
            $new_node = new ListNode($slow->val);
            $qian_tail->next = $new_node;
            $qian_tail = $new_node;
            $slow = $slow->next;
            $fast = $fast->next->next;
        }
        $mid = $slow;
        $right = $slow->next;
        $mid->next = null;
        $root = new TreeNode($mid->val);
        $root->left = self::sortedListToBST($qian_head->next);
        $root->right = self::sortedListToBST($right);
        return $root;
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