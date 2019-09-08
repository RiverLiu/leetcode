# longest-palindromic-substring 最长的回文字符串

- [题目链接](https://leetcode.com/problems/longest-palindromic-substring/submissions/)
- [领扣链接](https://leetcode-cn.com/problems/longest-palindromic-substring/submissions/)
- [tag] Medium, Array, Dynamic Programming


# 解法一：暴力法

依次比较字符串是否是回文，我提交的代码.

```java
    public String longestPalindrome(String s) {
        int maxLength = 0;
        String subString = "";
        
        int length = s.length();
        for (int idx = 0; idx < length; ++idx) {
            if (length - idx <= maxLength) {
                return subString;
            }
            
            int left = idx;
            for (int right = length - 1; right >= left + maxLength; --right) {
                int j = right;
                while (s.charAt(left) == s.charAt(j) && j > left) {
                    --j;
                    ++left;
                }
                
                if (j == left || j < left) {
                    if (right + 1 - idx > maxLength) {
                        maxLength = right - idx;
                        subString = s.substring(idx, right + 1);   
                    }
                } else {
                    left = idx;
                }
            }
        }
        
        return subString;
    }
```

**复杂度分析**

- 时间复杂度： `$O(n^3)$` 3层循环
- 空间复杂度：`$O(1)$`

# 解法二 动态规划

如果对于字符串 `bab` 是回文字符串，那么字符串 `ababa` 一定是回文字符串，因为首尾字符都是 `a`. 我们定义 `$P(i, j)$` 表示下标`$[i,j]` 的字符串

```math
P(i, j) = \
```

因此

```math
P(i, j) = (P(i+1, j-1) and S_i == S_j)
```

最初的例子为

```math
P(i, i) = true
P(i, i+1) = (S_i == S_{i+1})
```

实现算法为:

```java
public String longestPalindrome(String s) {
  int n = s.length();
  String res = null;
    
  boolean[][] dp = new boolean[n][n];
    
  for (int i = n - 1; i >= 0; i--) {
    for (int j = i; j < n; j++) {
      System.out.println("i => " + i + "\tj => " + j); 
      dp[i][j] = s.charAt(i) == s.charAt(j) && (j - i < 3 || dp[i + 1][j - 1]);
            
      if (dp[i][j] && (res == null || j - i + 1 > res.length())) {
        res = s.substring(i, j + 1);
      }
    }
  }
    
  return res;
}
```

其中，`j - i < 3` 需要特别说明一下：

- 当 `j - i = 0` 时，表示空字符串，是回文字符串
- 当 `j - i = 1` 时，表示单个字符串，是回文字符串
- 当 `j - i = 2` 时，即前面的表达式 `s.chartAt(i) == s.charAt(j)`

**复杂度分析:**

- 时间复杂度: `$O(n^2)$` 两层 for 循环
- 空间复杂度: `$O(n^2)$` 存储 dp 数组

# 解法三： 中心扩展法(官方算法)

我们观察到回文中心的两侧互为镜像。因此，回文可以从它的中心展开，并且只有 `$2n - 1$` 个这样的中心。

你可能会问，为什么会是 `$2n - 1$` 个，而不是 `$n$` 个中心？原因在于所含字母数为偶数的回文的中心可以处于两字母之间（例如 `$\textrm{"abba"}$` 的中心在两个 `$\textrm{'b'}$`之间）。

```java

public String longestPalindrome(String s) {
    if (s == null || s.length() < 1) return "";
    int start = 0, end = 0;
    for (int i = 0; i < s.length(); i++) {
        int len1 = expandAroundCenter(s, i, i);
        int len2 = expandAroundCenter(s, i, i + 1);
        int len = Math.max(len1, len2);
        if (len > end - start) {
            start = i - (len - 1) / 2;
            end = i + len / 2;
        }
    }
    return s.substring(start, end + 1);
}

private int expandAroundCenter(String s, int left, int right) {
    int L = left, R = right;
    while (L >= 0 && R < s.length() && s.charAt(L) == s.charAt(R)) {
        L--;
        R++;
    }
    return R - L - 1;
}
```

**复杂度分析**

- 时间复杂度：`$O(n^2)$` 由于围绕中心来扩展回文会耗去 O(n)O(n) 的时间，所以总的复杂度为 `$O(n^2)$`
- 空间复杂度：`$O(1)$`

# 解法四： Manacher's Alogrithm

中文翻译是马拉车算法。

TODO： 需要再花时间理解这个算法： https://segmentfault.com/a/1190000008484167

算法可视化： http://manacher-viz.s3-website-us-east-1.amazonaws.com/#/


以及复杂度的计算规则。

# 参考

- [刘毅 -- Manacher算法](https://segmentfault.com/a/1190000008484167)
