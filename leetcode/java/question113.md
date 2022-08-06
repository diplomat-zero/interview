```
给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径。

叶子节点 是指没有子节点的节点。

 

示例 1：


输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
示例 2：


输入：root = [1,2,3], targetSum = 5
输出：[]
示例 3：

输入：root = [1,2], targetSum = 0
输出：[]
 

提示：

树中节点总数在范围 [0, 5000] 内
-1000 <= Node.val <= 1000
-1000 <= targetSum <= 1000
```

```

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
    List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        LinkedList<Integer> trace = new LinkedList<>();
        dfs(root, targetSum, trace);
        return res;
    }

    public void dfs(TreeNode root, int targetSum, LinkedList<Integer> trace) {
        if (root == null) {
            return;
        }
        if (root.left == null && root.right == null) {
            if (root.val == targetSum) {
                trace.offerLast(root.val);
                res.add(new ArrayList<Integer>(trace));
                trace.pollLast();
                return;
            }
        }

        trace.offerLast(root.val);
        dfs(root.left, targetSum - root.val, trace);
        trace.pollLast();

        trace.offerLast(root.val);
        dfs(root.right, targetSum - root.val, trace);
        trace.pollLast();
    }
}
```