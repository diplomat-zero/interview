```
给定单个链表的头 head ，使用 插入排序 对链表进行排序，并返回 排序后链表的头 。

插入排序 算法的步骤:

插入排序是迭代的，每次只移动一个元素，直到所有元素可以形成一个有序的输出列表。
每次迭代中，插入排序只从输入数据中移除一个待排序的元素，找到它在序列中适当的位置，并将其插入。
重复直到所有输入数据插入完为止。
下面是插入排序算法的一个图形示例。部分排序的列表(黑色)最初只包含列表中的第一个元素。每次迭代时，从输入数据中删除一个元素(红色)，并就地插入已排序的列表中。

对链表进行插入排序。

示例 1：
输入: head = [4,2,1,3]
输出: [1,2,3,4]

示例 2：
输入: head = [-1,5,3,4,0]
输出: [-1,0,3,4,5]
 
提示：
列表中的节点数在 [1, 5000]范围内
-5000 <= Node.val <= 5000
```

```
思路
先找到待插入的结点（前一个结点值比当前的大），移除，移除前保存。
将该结点插入到合适的位置——从头遍历比较，并插入。

图例
cur 指针扫描整个链表，如果 cur.val <= cur.next.val，继续推进


dummy      cur      cur.next  
  0   ->   -1    ->    5     ->     3     ->     4     ->    0
直到 cur.val > cur.next.val ，找到 cur.next，删除前保存给 temp。


dummy                 cur        cur.next   cur.next.next
  0   ->   -1    ->    5     ->     3     ->     4     ->    0
删除后：


dummy                 cur       cur.next  
  0   ->   -1    ->    5     ->     4     ->    0
temp
  3   ->   4   ->   0
现在要找插入的位置。设置虚拟头结点是因为，它可能插入成为链表头，为了与插入到别的位置的操作一致，给头结点加一个前置结点。

用 prev 指针去推进，初始指向 dummy，如果 prev.next.val <= temp.val，继续推进


prev 
dummy    prev.next     
  0   ->    -1    ->     5    ->    4     ->    0
temp
  3   ->   4   ->   0
一旦 prev.next.val > temp.val ，temp 插入到 prev 和 prev.next 之间


dummy      prev      prev.next    
  0   ->    -1    ->     5    ->    4     ->    0

dummy      prev       temp     prev.next    
  0   ->    -1    ->    3    ->    5    ->    4    ->    0
这样就完成了一个“不对”的结点的插入，遍历整个链表，重复做这些事。
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
    function insertionSortList($head) {
        $dummy = new ListNode(-10000);
        $dummy->next = $head;

        $cur = $head;

        while ($cur != null && $cur->next != null) {
            if ($cur->val <= $cur->next->val) {
                $cur = $cur->next;
            } else {
                $tmp = $cur->next;
                $cur->next = $cur->next->next;

                $prev = $dummy;
                while ($prev->next->val < $tmp->val) {
                    $prev = $prev->next;
                }
                $tmp->next = $prev->next;
                $prev->next = $tmp;
            }
        }
        return $dummy->next;
    }
}
```