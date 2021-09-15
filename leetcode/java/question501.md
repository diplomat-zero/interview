```
给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

结点左子树中所含结点的值小于等于当前结点的值
结点右子树中所含结点的值大于等于当前结点的值
左子树和右子树都是二叉搜索树
例如：
给定 BST [1,null,2,2],

   1
    \
     2
    /
   2
返回[2].

提示：如果众数超过1个，不需考虑输出顺序

进阶：你可以不使用额外的空间吗？（假设由递归产生的隐式调用栈的开销不被计算在内）
```

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int[] findMode(TreeNode root) {

        Map<Integer, Integer> map = new HashMap<>();
        inorder(root, map);

        int max = 0;
        ArrayList<Integer> ret = new ArrayList<>();
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            int key = entry.getKey();
            int value = entry.getValue();
            if (ret.size() == 0) {
                ret.add(key);
                max = value;
            } else {
                if (value > max) {
                    max = value;
                    ret.clear();
                    ret.add(key);
                } else if (value == max) {
                    ret.add(key);
                }
            }
        }

        int[] mode = new int[ret.size()];
        for (int i = 0; i < ret.size(); ++i) {
            mode[i] = ret.get(i);
        }
        return mode;
    }

    public void inorder(TreeNode root, Map<Integer, Integer> ret) {
        if (root == null) {
            return;
        }

        inorder(root.left, ret);
        if (ret.containsKey(root.val)) {
            ret.put(root.val, ret.get(root.val) + 1);
        } else {
            ret.put(root.val, 1);
        }
        inorder(root.right, ret);

    }
}
```