```
给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

 

示例 1：

输入：s = "3[a]2[bc]"
输出："aaabcbc"
示例 2：

输入：s = "3[a2[c]]"
输出："accaccacc"
示例 3：

输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"
示例 4：

输入：s = "abc3[cd]xyz"
输出："abccdcdcdxyz"
 

提示：

1 <= s.length <= 30
s 由小写英文字母、数字和方括号 '[]' 组成
s 保证是一个 有效 的输入。
s 中所有整数的取值范围为 [1, 300] 
```

```

```

```
func decodeString(s string) string {
    stack := make([]string, 0)
	for i := 0; i < len(s); i++ {
		str_char := string(s[i])
		if str_char == "]" {
			str_str := ""
			end_str := stack[len(stack) - 1]
			for end_str != "[" {
				str_str = end_str + str_str
				stack = stack[:len(stack) - 1]
				end_str = stack[len(stack) - 1]
			}
			stack = stack[:len(stack) - 1]
			num_str := ""
			end_num := stack[len(stack) - 1]
			for end_num >= "0" && end_num <= "9" {
				num_str = end_num + num_str
				stack = stack[:len(stack) - 1]
				if len(stack) == 0 {
					break
				}
				end_num = stack[len(stack) - 1]
			}
			num_int, _ := strconv.Atoi(num_str)
			res_str := ""
			for i := 0; i < num_int; i++ {
				res_str += str_str
			}
			stack = append(stack, res_str)
		} else {
			stack = append(stack, str_char)
		}
	}
	result := ""
	for i := 0; i < len(stack); i++ {
		result += stack[i]
	}
    return result
}
```