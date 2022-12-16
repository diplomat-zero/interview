```
给定 s 和 t 两个字符串，当它们分别被输入到空白的文本编辑器后，如果两者相等，返回 true 。# 代表退格字符。

注意：如果对空文本输入退格字符，文本继续为空。

 

示例 1：

输入：s = "ab#c", t = "ad#c"
输出：true
解释：s 和 t 都会变成 "ac"。
示例 2：

输入：s = "ab##", t = "c#d#"
输出：true
解释：s 和 t 都会变成 ""。
示例 3：

输入：s = "a#c", t = "b"
输出：false
解释：s 会变成 "c"，但 t 仍然是 "b"。
 

提示：

1 <= s.length, t.length <= 200
s 和 t 只含有小写字母以及字符 '#'
 

进阶：

你可以用 O(n) 的时间复杂度和 O(1) 的空间复杂度解决该问题吗？
```

```

```

```
func backspaceCompare(s string, t string) bool {
    stackS := make([]string, 0)
    stackT := make([]string, 0)
    for _,value := range s {
        charS := string(value)
        if charS == "#" {
            if len(stackS) != 0 {
                stackS = stackS[:len(stackS) - 1]
            }
        } else {
            stackS = append(stackS, charS)
        }
    }
    for _,value := range t {
        charT := string(value)
        if charT == "#" {
            if len(stackT) != 0 {
                stackT = stackT[:len(stackT) - 1]
            }
        } else {
            stackT = append(stackT, charT)
        }
    }
    if len(stackS) != len(stackT) {
        return false
    }
    i := 0
    j := 0
    for i < len(stackS) && j < len(stackT) {
        charS := stackS[i]
        charT := stackT[j]
        if charS != charT {
            return false
        }
        i++
        j++
    }
    return true

}
```