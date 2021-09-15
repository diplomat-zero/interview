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
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
var m map[int]int
var ret []int
func findMode(root *TreeNode) []int {
    m = make(map[int]int)
    inorder(root)
    
    ret = make([]int, 0)
    var max int
    for k, v := range m {
        if len(ret) == 0 {
            ret = append(ret, k)
            max = v
        } else {
            if v > max {
                max = v
                ret = ret[0:0]
                ret = append(ret, k)
            } else if v == max {
                ret = append(ret, k)
            }
        }
    }

    return ret
}

func inorder(root *TreeNode) {
    if root == nil {
        return 
    }

    inorder(root.Left)
    if _, ok := m[root.Val]; ok {
            m[root.Val] += 1
        } else {
            m[root.Val] = 1
        }
    inorder(root.Right)
}
```