```
给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

注意：若 s 和 t 中每个字符出现的次数都相同，则称 s 和 t 互为字母异位词。

 

示例 1:

输入: s = "anagram", t = "nagaram"
输出: true
示例 2:

输入: s = "rat", t = "car"
输出: false
 

提示:

1 <= s.length, t.length <= 5 * 104
s 和 t 仅包含小写字母
 

进阶: 如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？
```

```

```

```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        s_map = {}
        for i in range(len(s)):
            if s[i] in s_map:
                s_map[s[i]] += 1
            else:
                s_map[s[i]] = 1
        
        for j in range(len(t)):
            if t[j] not in s_map:
                return False
            s_map[t[j]] -= 1
            if s_map[t[j]] < 0:
                return False
        
        for m in s_map:
            if s_map[m] != 0:
                return False
        
        return True
```