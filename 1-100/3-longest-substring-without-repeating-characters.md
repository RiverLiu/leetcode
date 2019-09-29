# Longest Substring Without Repeating Characters 无重复字符的最长子串

tags: Medium, String, Hash Table, Silding Window

- [题目链接](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [领扣链接](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

从字符串中找出不重复的最长子串。

# 解法一： 暴力法

暴力法是依次查找字符串的子串中，是否有重复的字符串，时间复杂度过高，可能通过测试。

# 解法二：滑动窗口

先看下，我提交的代码，解题思路是这样的(和官方解法三很相似，但是，但是，代码写法没有官方优雅 :-<)：

1. 从数组尾部开始向前遍历数组，用一个额外数组 `tables` 存储已经存在的值，数组下标表示元素ASCII值，值表示是数组元素对应的下标值。
2. 遍历时，查看当前元素是否在 tables 中(查看 tables 中，元素的 ASCII 值对应的元素是否为0，0 表示不存在，1表示存在)，
  - 如果不在，继续向前遍历
  - 如果存在，检查当前长度是否是最大的，因为 tables 中记录了元素的下标值，则对应下标值之后的元素可以跳过不用比较


```java
public int lengthOfLongestSubstring(String s) {
    int[] tables = new int[256];
    int length = s.length();
    if (length <= 1) {
        return length;
    }

    int max = 0;  
    int len = 0;
    int idx;
    for (int i = length - 1; i >= 0; --i) {
        char c = s.charAt(i);
        idx = tables[(int)c];
        if (idx > 0) {
            // already exists
            for (int j = 1, offset = len - (idx - i);  j <= offset; ++j) {
                tables[(int)s.charAt(idx + j)] = 0;
            }
            if (len > max) {
                max = len;
            }
            len = idx - i;
        } else {
            ++len;
        }
        tables[(int)c] = i;
    }
    
    return Math.max(len, max);
}
```

直接把官方解法中，对滑动窗口的解释复制过来，如下

>在暴力法中，我们会反复检查一个子字符串是否含有有重复的字符，但这是没有必要的。如果从索引 $$i$$ 到 $$j - 1$$ 之间的子字符串 $$s_{ij}$$ 已经被检查为没有重复字符。我们只需要检查 $$s[j]$$ 对应的字符是否已经存在于子字符串 $$s_{ij}$$ 中。
>
>要检查一个字符是否已经在子字符串中，我们可以检查整个子字符串，这将产生一个复杂度为 $$O(n^2)$$ 的算法，但我们可以做得更好。
>通过使用 HashSet 作为滑动窗口，我们可以用 $$O(1)$$ 的时间来完成对字符是否在当前的子字符串中的检查。
>
>滑动窗口是数组/字符串问题中常用的抽象概念。 窗口通常是在数组/字符串中由开始和结束索引定义的一系列元素的集合，即 $$[i, j)$$（左闭，右开）。而滑动窗口是可以将两个边界向某一方向“滑动”的窗口。例如，我们将 $$[i, j)$$ 向右滑动 $$1$$ 个元素，则它将变为 $$[i+1, j+1)$$（左闭，右开）。
>
>回到我们的问题，我们使用 HashSet 将字符存储在当前窗口 $$[i, j)$$（最初 $$j = i$$）中。 然后我们向右侧滑动索引 $$j$$，如果它不在 HashSet 中，我们会继续滑动 $$j$$。直到 $$s[j]$$ 已经存在于 HashSet 中。此时，我们找到的没有重复字符的最长子字符串将会以索引 $$i$$ 开头。如果我们对所有的 $$i$$ 这样做，就可以得到答案。

```java
public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        Set<Character> set = new HashSet<>();
        int ans = 0, i = 0, j = 0;
        while (i < n && j < n) {
            // try to extend the range [i, j]
            if (!set.contains(s.charAt(j))){
                set.add(s.charAt(j++));
                ans = Math.max(ans, j - i);
            }
            else {
                set.remove(s.charAt(i++));
            }
        }
        return ans;
    }
```

**复杂度分析**

- 时间复杂度：$$O(2n) = O(n)$$，在最糟糕的情况下，每个字符将被 $$i$$ 和 $$j$$ 访问两次。
- 空间复杂度：$$O(min(m, n))$$，与之前的方法相同。滑动窗口法需要 $$O(k)$$ 的空间，其中 $$k$$ 表示 Set 的大小。而 Set 的大小取决于字符串 $$n$$ 的大小以及字符集 / 字母 $$m$$ 的大小。

# 解法三：优化的滑动窗口(官方方法)

上述的方法最多需要执行 2n 个步骤。事实上，它可以被进一步优化为仅需要 n 个步骤。我们可以定义字符到索引的映射，而不是使用集合来判断一个字符是否存在。 当我们找到重复的字符时，我们可以立即跳过该窗口。

也就是说，如果 $$s[j]$$ 在 $$[i, j)$$ 范围内有与 $$j'$$ 重复的字符，我们不需要逐渐增加 $$i$$。 我们可以直接跳过 $$[i, j']$$ 范围内的所有元素，并将 $$i$$ 变为 $$j' + 1$$.

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        Map<Character, Integer> map = new HashMap<>(); // current index of character
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            ans = Math.max(ans, j - i + 1);
            map.put(s.charAt(j), j + 1);
        }
        return ans;
    }
}
```
