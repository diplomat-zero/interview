```
给你一个字符串表达式 s ，请你实现一个基本计算器来计算并返回它的值。

整数除法仅保留整数部分。

你可以假设给定的表达式总是有效的。所有中间结果将在 [-231, 231 - 1] 的范围内。

注意：不允许使用任何将字符串作为数学表达式计算的内置函数，比如 eval() 。

 

示例 1：

输入：s = "3+2*2"
输出：7
示例 2：

输入：s = " 3/2 "
输出：1
示例 3：

输入：s = " 3+5 / 2 "
输出：5
 

提示：

1 <= s.length <= 3 * 105
s 由整数和算符 ('+', '-', '*', '/') 组成，中间由一些空格隔开
s 表示一个 有效表达式
表达式中的所有整数都是非负整数，且在范围 [0, 231 - 1] 内
题目数据保证答案是一个 32-bit 整数
```

```

```

```
class Solution {
    int index = 0;
    public int calculate(String s) {
        int num = 0;
        char sign = '+';
        LinkedList<Integer> stack = new LinkedList<>();

        for (; index < s.length(); index++) {
            char cur = s.charAt(index);
            if (Character.isDigit(cur)) {
                num = 10 * num + (cur - '0');
            } else if (cur == '(') {
                index++;
                num = calculate(s);
            }
            
            if ((!Character.isDigit(cur) && cur != ' ') || index == s.length() - 1) {
                if (sign == '+') {
                    stack.offerLast(num);
                } else if (sign == '-') {
                    stack.offerLast(-num);
                } else if (sign == '*') {
                    stack.offerLast(stack.pollLast() * num);
                } else if (sign == '/') {
                    stack.offerLast(stack.pollLast() / num);
                }
                num = 0;
                sign = cur;
            }
            
            if (cur == ')') {
                break;
            }
        }

        int res = 0;
        for (Integer value : stack) {
            res += value;
        }

        return res;
    }
}
```