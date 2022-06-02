```
有 n 个人被分成数量未知的组。每个人都被标记为一个从 0 到 n - 1 的唯一ID 。

给定一个整数数组 groupSizes ，其中 groupSizes[i] 是第 i 个人所在的组的大小。例如，如果 groupSizes[1] = 3 ，则第 1 个人必须位于大小为 3 的组中。

返回一个组列表，使每个人 i 都在一个大小为 groupSizes[i] 的组中。

每个人应该 恰好只 出现在 一个组 中，并且每个人必须在一个组中。如果有多个答案，返回其中 任何 一个。可以 保证 给定输入 至少有一个 有效的解。

示例 1：
输入：groupSizes = [3,3,3,3,3,1,3]
输出：[[5],[0,1,2],[3,4,6]]
解释：
第一组是 [5]，大小为 1，groupSizes[5] = 1。
第二组是 [0,1,2]，大小为 3，groupSizes[0] = groupSizes[1] = groupSizes[2] = 3。
第三组是 [3,4,6]，大小为 3，groupSizes[3] = groupSizes[4] = groupSizes[6] = 3。 
其他可能的解决方案有 [[2,1,6],[5],[0,4,3]] 和 [[5],[0,6,2],[4,3,1]]。

示例 2：
输入：groupSizes = [2,1,3,3,3,2]
输出：[[1],[0,5],[2,3,4]]
 
提示：
groupSizes.length == n
1 <= n <= 500
1 <= groupSizes[i] <= n
```

```
对于两个用户 x 和 y，如果 groupSize[x] != groupSize[y]，它们用户组的大小不同，那么它们一定不在同一个用户组中。因此我们可以首先对所有的用户进行一次【粗分组】，用一个哈希映射（HashMap）来存储所有的用户。哈希映射中键值对为 (gsize, users)，其中 gsize 表示用户组的大小，users 表示满足用户组大小为 gsize，即 groupSize[x] == gsize 的所有用户。这样以来，我们就把所有用户组大小相同的用户都暂时放在了同一个组中。

在进行了【粗分组】后，我们可以将每个键值对 (gsize, users) 中的 users 进行【细分组】。由于题目保证了给出的数据至少存在一种方案，因此我们的【细分组】可以变得很简单：只要每次从 users 中取出 gsize 个用户，把它们放在一个组中就可以了。在进行完所有的【细分组】后，我们就得到了一种满足条件的分组方案。
```

```
class Solution {

    /**
     * @param Integer[] $groupSizes
     * @return Integer[][]
     */
    function groupThePeople($groupSizes) {
        $len = count($groupSizes);
        $res = [];
        for ($i = 0; $i < $len; $i++) {
            $res[$groupSizes[$i]][] = $i;
        }
        $ret = [];
        foreach ($res as $size => $value) {
            for ($i = 0; $i < count($value) / $size ;$i++) {
                $ret[] = array_slice($value, $i * $size, $size);
            }
        }
        return $ret;
    }
}
```