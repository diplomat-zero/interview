```
给你一棵二叉树的根节点 root ，树中有 n 个节点，每个节点都有一个不同于其他节点且处于 1 到 n 之间的值。
另给你一个由 n 个值组成的行程序列 voyage ，表示 预期 的二叉树 先序遍历 结果。
通过交换节点的左右子树，可以 翻转 该二叉树中的任意节点。例，翻转节点 1 的效果如下：
请翻转 最少 的树中节点，使二叉树的 先序遍历 与预期的遍历行程 voyage 相匹配 。 
如果可以，则返回 翻转的 所有节点的值的列表。你可以按任何顺序返回答案。如果不能，则返回列表 [-1]。

示例 1：
输入：root = [1,2], voyage = [2,1]
输出：[-1]
解释：翻转节点无法令先序遍历匹配预期行程。

示例 2：
输入：root = [1,2,3], voyage = [1,3,2]
输出：[1]
解释：交换节点 2 和 3 来翻转节点 1 ，先序遍历可以匹配预期行程。

示例 3：
输入：root = [1,2,3], voyage = [1,2,3]
输出：[]
解释：先序遍历已经匹配预期行程，所以不需要翻转节点。
 
提示：
树中的节点数目为 n
n == voyage.length
1 <= n <= 100
1 <= Node.val, voyage[i] <= n
树中的所有值 互不相同
voyage 中的所有值 互不相同
```

```
思路
采用DFS策略，分情况讨论：
情况1：树为空，肯定匹配，返回true；
情况2：如果当前访问的结点和先序序列数组中对应值不相等，那肯定不匹配，返回false；
情况3：如果当前结点对应上了，就要检查左右子树是否匹配，先左后右（先序）；
情况4：如果左右子树不匹配，那就翻转，先右后左去检查是否匹配，如果匹配，则把当前root的值放入res；
情况5：如果翻转过后还是不匹配，返回false；
```

```
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
     * @param TreeNode $root
     * @param Integer[] $voyage
     * @return Integer[]
     */
    function flipMatchVoyage($root, $voyage) {
        $i = 0;
        $res = [];
        if ($this->dfstree($root, $voyage, $i, $res)) {
            return $res;
        }
        return [-1];
    }

    function dfstree($root, $voyage, &$i, &$res) {
        if ($root == null) {
            return true;
        }
        if ($root->val != $voyage[$i]) {
            return false;
        }

        $i++;
        if ($this->dfstree($root->left, $voyage, $i, $res) && $this->dfstree($root->right, $voyage, $i, $res)) {
            return true;
        }
        if ($this->dfstree($root->right, $voyage, $i, $res) && $this->dfstree($root->left, $voyage, $i, $res)) {
            $res[] = $root->val;
            return true;
        }
        return false;
    }
}
```