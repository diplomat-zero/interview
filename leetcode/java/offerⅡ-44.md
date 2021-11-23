```
给定一棵二叉树的根节点 root ，请找出该二叉树中每一层的最大值。

示例1：
输入: root = [1,3,2,5,3,null,9]
输出: [1,3,9]
解释:
          1
         / \
        3   2
       / \   \  
      5   3   9 

示例2：
输入: root = [1,2,3]
输出: [1,3]
解释:
          1
         / \
        2   3

示例3：
输入: root = [1]
输出: [1]

示例4：
输入: root = [1,null,2]
输出: [1,2]
解释:      
           1 
            \
             2     

示例5：
输入: root = []
输出: []

提示：

二叉树的节点个数的范围是 [0,104]
-231 <= Node.val <= 231 - 1
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
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) {
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int tmp = Integer.MIN_VALUE;
            for (int i = queue.size(); i > 0; i--) {
                TreeNode node = queue.poll();
                tmp = Math.max(tmp, node.val);
                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            }
            result.add(tmp);
        }

        return result;
    }
}
```