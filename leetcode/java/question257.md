```
给定一个二叉树，返回所有从根节点到叶子节点的路径。
说明: 叶子节点是指没有子节点的节点。

示例:
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]
解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList<>();
        List<TreeNode> trace = new ArrayList<>();
        trace.add(root);

        dfs(root, result, trace);
        return result;
    }

    public void dfs(TreeNode root, List<String> result, List<TreeNode> trace) {
        if (root.left == null && root.right == null) {
            StringBuilder tmp = new StringBuilder();
            for (TreeNode treeNode : trace) {
                tmp.append(treeNode.val);
                tmp.append("->");
            }
            tmp = new StringBuilder(tmp.substring(0, tmp.length() - 2));
            result.add(tmp.toString());
        }

        if (root.left != null) {
            if (!trace.contains(root.left)) {
                trace.add(root.left);
                dfs(root.left, result, trace);
                trace.remove(root.left);
            }
        }

        if (root.right != null) {
            if (!trace.contains(root.right)) {
                trace.add(root.right);
                dfs(root.right, result, trace);
                trace.remove(root.right);
            }
        }
    }
}
```