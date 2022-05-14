```
给定一个 N 叉树，返回其节点值的层序遍历。（即从左到右，逐层遍历）。

树的序列化输入是用层序遍历，每组子节点都由 null 值分隔（参见示例）。

示例 1：
输入：root = [1,null,3,2,4,null,5,6]
输出：[[1],[3,2,4],[5,6]]

示例 2：
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：[[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
 
提示：
树的高度不会超过 1000
树的节点总数在 [0, 10^4] 之间
```

```
/**
 * Definition for a Node.
 * class Node {
 *     public $val = null;
 *     public $children = null;
 *     function __construct($val = 0) {
 *         $this->val = $val;
 *         $this->children = array();
 *     }
 * }
 */

class Solution {
    /**
     * @param Node $root
     * @return integer[][]
     */
    function levelOrder($root) {
        if ($root == null) {
            return [];
        }
		$result = [];
        $queue[] = $root;
        while (!empty($queue)) {
            $cnt = count($queue);
            $ceng = [];
            for ($i = 0; $i < $cnt; $i++) {
                $node = array_shift($queue);
                for ($j = 0; $j < count($node->children); $j++) {
                    $queue[] = $node->children[$j];
                }
                $ceng[] = $node->val;
            }
            $result[] = $ceng;
        }
        return $result;
    }
}
```