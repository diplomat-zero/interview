```
给你一个字符串表达式 s ，请你实现一个基本计算器来计算并返回它的值。

注意:不允许使用任何将字符串作为数学表达式计算的内置函数，比如 eval() 。

 

示例 1：

输入：s = "1 + 1"
输出：2
示例 2：

输入：s = " 2-1 + 2 "
输出：3
示例 3：

输入：s = "(1+(4+5+2)-3)+(6+8)"
输出：23
 

提示：

1 <= s.length <= 3 * 105
s 由数字、'+'、'-'、'('、')'、和 ' ' 组成
s 表示一个有效的表达式
'+' 不能用作一元运算(例如， "+1" 和 "+(2 + 3)" 无效)
'-' 可以用作一元运算(即 "-1" 和 "-(2 + 3)" 是有效的)
输入中不存在两个连续的操作符
每个数字和运行的计算将适合于一个有符号的 32位 整数
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