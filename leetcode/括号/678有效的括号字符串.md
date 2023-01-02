```
给定一个只包含三种字符的字符串：（ ，） 和 *，写一个函数来检验这个字符串是否为有效字符串。有效字符串具有如下规则：

任何左括号 ( 必须有相应的右括号 )。
任何右括号 ) 必须有相应的左括号 ( 。
左括号 ( 必须在对应的右括号之前 )。
* 可以被视为单个右括号 ) ，或单个左括号 ( ，或一个空字符串。
一个空字符串也被视为有效字符串。
示例 1:

输入: "()"
输出: True
示例 2:

输入: "(*)"
输出: True
示例 3:

输入: "(*))"
输出: True
注意:

字符串大小将在 [1，100] 范围内。
```

```

```

```
func checkValidString(s string) bool {
    stack1 := make([]int, 0)
    stack2 := make([]int, 0)
    for i, value := range s {
        char := string(value)
        if char == "(" {
            stack1 = append(stack1, i)
        } else if char == "*" {
            stack2 = append(stack2, i)
        } else {
            if len(stack1) != 0 {
                stack1 = stack1[:len(stack1) - 1]
            } else if len(stack2) != 0 {
                stack2 = stack2[:len(stack2) - 1]
            } else {
                return false
            }
        }
    }
    if len(stack1) == 0 && len(stack2) == 0 {
        return true
    } else if len(stack1) != 0 && len(stack2) == 0 {
        return false
    } else if len(stack1) == 0 && len(stack2) != 0 {
        return true
    } else {
        if len(stack1) > len(stack2) {
            return false
        }
        for len(stack1) > 0 {
            stack1_last := stack1[len(stack1) - 1]
            stack1 = stack1[:len(stack1) - 1]
            stack2_last := stack2[len(stack2) - 1]
            stack2 = stack2[:len(stack2) - 1]
            if stack1_last > stack2_last {
                return false
            }
        }
        return true
    }
}
```