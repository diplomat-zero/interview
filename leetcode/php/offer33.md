```
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。

 参考以下这颗二叉搜索树：

     5
    / \
   2   6
  / \
 1   3

示例 1：
输入: [1,6,3,2,5]
输出: false

示例 2：
输入: [1,3,2,6,5]
输出: true
 
提示：
数组长度 <= 1000
```

```
class Solution {

    /**
     * @param Integer[] $postorder
     * @return Boolean
     */
    function verifyPostorder($postorder) {
        return $this->help($postorder, 0, count($postorder) - 1);
    }

    function help($postorder, $left, $right) {
        if ($left >= $right) {
            return true;
        }
        $start = $left;
        while ($postorder[$start] < $postorder[$right]) $start++;
        $end = $start;
        while ($postorder[$end] > $postorder[$right]) $end++;

        return $end == $right && $this->help($postorder, $left, $start - 1) && $this->help($postorder, $start, $right - 1);
    }
}
```