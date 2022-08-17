```
给定一个可包含重复数字的序列 nums ，按任意顺序 返回所有不重复的全排列。

 

示例 1：

输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
示例 2：

输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
 

提示：

1 <= nums.length <= 8
-10 <= nums[i] <= 10
```

```

```

```
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    boolean[] used;
    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        LinkedList<Integer> trace = new LinkedList<>();
        used = new boolean[nums.length];
        dfs(nums, trace);
        return res;
    }

    public void dfs(int[] nums, LinkedList<Integer> trace) {
        if (nums.length == trace.size()) {
            res.add(new LinkedList<>(trace));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (used[i]) {
                continue;
            }
            if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
                continue;
            }
            trace.addLast(nums[i]);
            used[i] = true;
            dfs(nums, trace);
            trace.pollLast();
            used[i] = false;
        }
    }
}
```