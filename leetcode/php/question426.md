```
将一个 二叉搜索树 就地转化为一个 已排序的双向循环链表 。

对于双向循环列表，你可以将左右孩子指针作为双向循环链表的前驱和后继指针，第一个节点的前驱是最后一个节点，最后一个节点的后继是第一个节点。

特别地，我们希望可以 就地 完成转换操作。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继。还需要返回链表中最小元素的指针。

示例 1：
输入：root = [4,2,5,1,3] 
输出：[1,2,3,4,5]

示例 2：
输入：root = [2,1,3]
输出：[1,2,3]

示例 3：
输入：root = []
输出：[]
解释：输入是空树，所以输出也是空链表。

示例 4：
输入：root = [1]
输出：[1]
 
提示：

-1000 <= Node.val <= 1000
Node.left.val < Node.val < Node.right.val
Node.val 的所有值都是独一无二的
0 <= Number of Nodes <= 2000
```

```
在遍历的过程中，有两个重要变量：

fristVisit：记录我们第一次遇到的节点。
用于连接链表的头结点和尾节点，使双向链表变成双向循环链表。
lastVisit：记录上一次遇到的节点。
在遍历的过程中，对lastVisit节点和当前节点(root)的左右指针进行连接。
```

```
/**
 * Definition for a Node.
 * class Node {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($val = 0) {
 *         $this->val = $val;
 *         $this->left = null;
 *         $this->right = null;
 *     }
 * }
 */

class Solution {
    /**
     * @param Node $root
     * @return Node
     */
    public $first;
    public $last;
    function treeToDoublyList($root) {
        if ($root == null) {
            return null;
        }
        $this->inorder($root);
        $this->first->left = $this->last;
        $this->last->right = $this->first;
        return $this->first;
    }

    function inorder($root) {
        if ($root == null) {
            return;
        }
        $this->inorder($root->left);
        if ($this->first == null) {
            $this->first = $root;
        }
        if ($this->last != null) {
            $root->left = $this->last;
            $this->last->right = $root;
        }
        $this->last = $root;
        $this->inorder($root->right);
    }
}
```