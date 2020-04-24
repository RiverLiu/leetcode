# 最长公共前缀

tags: Easy, String

- [题目链接](https://leetcode.com/problems/longest-common-prefix/)
- [领扣链接](https://leetcode-cn.com/problems/longest-common-prefix/)

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) {
            return "";
        }
        if (strs.length == 1) {
            return strs[0];
        }

        int i = 0;
        boolean goon = true;
        int length = strs[0].length();
        for (i = 0; i < length; ++i) {
            char c = strs[0].charAt(i);
            for (int j = 1; j < strs.length; ++j) {
                if (i == strs[j].length() || strs[j].charAt(i) != c) {
                    goon = false;
                    break;
                }
            }
            if (!goon) {
                break;
            }
        }

        return strs[0].substring(0, i);
    }
}
```

更简洁的写法

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) {
            return "";
        }

        int i = 0;
        int length = strs[0].length();
        for (i = 0; i < length; ++i) {
            char c = strs[0].charAt(i);
            for (int j = 1; j < strs.length; ++j) {
                if (i == strs[j].length() || strs[j].charAt(i) != c) {
                    return strs[0].substring(0, i);
                }
            }
        }

        return strs[0];
    }
}
```

另外一种解法

```java
public String longestCommonPrefix(String[] strs) {
    if(strs == null || strs.length == 0) return "";
    String pre = strs[0];
    int i = 1;
    while(i < strs.length){
        while(strs[i].indexOf(pre) != 0)
            pre = pre.substring(0,pre.length()-1);
        i++;
    }
    return pre;
}
```
