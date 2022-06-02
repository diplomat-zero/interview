```
给定一个长度为 n 的链表 head
对于列表中的每个节点，查找下一个 更大节点 的值。也就是说，对于每个节点，找到它旁边的第一个节点的值，这个节点的值 严格大于 它的值。
返回一个整数数组 answer ，其中 answer[i] 是第 i 个节点( 从1开始 )的下一个更大的节点的值。如果第 i 个节点没有下一个更大的节点，设置 answer[i] = 0 。

示例 1：
输入：head = [2,1,5]
输出：[5,5,0]

示例 2：
输入：head = [2,7,4,3,5]
输出：[7,0,5,5,0]
 
提示：
链表中节点数为 n
1 <= n <= 104
1 <= Node.val <= 109
```

```

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
     * @return Integer[]
     */
    function nextLargerNodes($head) {
        $nums = [];
        while ($head != null) {
            $nums[] = $head->val;
            $head = $head->next;
        }

        $stack = [];
        $res = [];
        for ($i = count($nums) - 1; $i >= 0; $i--) {
            while (!empty($stack) && end($stack) <= $nums[$i]) {
                array_pop($stack);
            }
            $ret = empty($stack) ? 0 : end($stack);
            array_unshift($res, $ret);
            $stack[] = $nums[$i];
        }
        return $res;
    }
}
```