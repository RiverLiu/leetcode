# Z 字形变换

tags: String

- [题目链接](https://leetcode.com/problems/zigzag-conversion/submissions/)
- [领扣链接](https://leetcode-cn.com/problems/zigzag-conversion/submissions/)

## 解法一 按行排序

这是官方给出的解法，使用一组额外的列表存储字符串的值，列表的大小为 $$min(numRows, len(s))$$. 执行过程：遍历字符串，然后将第一个字符串放入第一个列表，第二个字符串放入第二个列表，依次类推，如果遇到第一行或者 `numRows` 行时，则将放入列表的顺序换成相反的方向。遍历完成后，将列表中的字符串拼接成一个字符串输出。

官方代码：

```java
class Solution {
    public String convert(String s, int numRows) {

        if (numRows == 1) return s;

        List<StringBuilder> rows = new ArrayList<>();
        for (int i = 0; i < Math.min(numRows, s.length()); i++)
            rows.add(new StringBuilder());

        int curRow = 0;
        boolean goingDown = false;

        for (char c : s.toCharArray()) {
            rows.get(curRow).append(c);
            if (curRow == 0 || curRow == numRows - 1) goingDown = !goingDown;
            curRow += goingDown ? 1 : -1;
        }

        StringBuilder ret = new StringBuilder();
        for (StringBuilder row : rows) ret.append(row);
        return ret.toString();
    }
}
```

代码中， 关键代码 `if (curRow == 0 || curRow == numRows - 1) goingDown = !goingDown; curRow += goingDown ? 1 : -1;` 根据方向，加或者减 1，得到下一个列表的索引。

**复杂度分析**

- 时间复杂度：程序中遍历字符串，时间复杂度为 $$O(n)$$
- 空间复杂度：使用了额外的列表，大小为 $$O(n), n = len(s)$$

## 解法二 按行访问

另外一种方法就是根据**Z**字形的形状计算每行每个元素的索引记录。具体怎么找规律，也是推算的(假定一个公式，然后带入数据进行计算)。

每一行的字符所在字符串的位置如下

- 行 `0` 中的字符位于索引 k 为 $$2 \cdot \text{numRows} - 2)$$ 处;
- 行 `numRows−1` 中的字符位于索引 k 为 $$2 \cdot \text{numRows} - 2) + \text{numRows} - 1$$ 处;
- 内部的 行 ii 中的字符位于索引 k 为 $$2 \cdot \text{numRows}-2)+i$$ 以及 (k+1) $$2 \cdot \text{numRows}-2)- i(k+1)$$ 处;

下面代码是我提交的，代码把第`0`行和`numRows-1`做单独处理了，看起来，代码写的很多内容。官方的解法比这个简单，官方解法使用了一个 `cycleLen` 每次循环增加的值，也就是说同一行，第 `k` 和 `k + 1` 索引是与 `cycleLen` 有关联的。

```java
class Solution {
    public String convert(String s, int numRows) {
        int length = s.length();
        if (length <= 1 || numRows == 1) {
            return s;
        }

        int left = 0;
        int right = 0;
        int round = length / 2 * (numRows - 1) + 1;
        StringBuilder sb = new StringBuilder(length);
        for (int i = 0; i < numRows; ++i) {
               if (i < length) {
                sb.append(s.charAt(i));
            }
            for (int j = 1; j < round; ++j) {
                left = 2 * j * (numRows - 1) - i;
                right = 2 * j * (numRows - 1) + i;

                // last row
                if (right - left == 2 * (numRows - 1)) {
                    if (right < length) {
                        sb.append(s.charAt(right));
                    }
                    continue;
                } else if (left < length) {
                    sb.append(s.charAt(left));
                } else {
                    break;
                }

                // first row
                if (left == right) {
                    continue;
                }

                // middle row
                if (right < length) {
                    sb.append(s.charAt(right));
                }
            }
        }

        return sb.toString();
    }
}
```

官方的代码

```java
class Solution {
    public String convert(String s, int numRows) {

        if (numRows == 1) return s;

        StringBuilder ret = new StringBuilder();
        int n = s.length();
        int cycleLen = 2 * numRows - 2;

        for (int i = 0; i < numRows; i++) {
            for (int j = 0; j + i < n; j += cycleLen) {
                ret.append(s.charAt(j + i));
                if (i != 0 && i != numRows - 1 && j + cycleLen - i < n)
                    ret.append(s.charAt(j + cycleLen - i));
            }
        }
        return ret.toString();
    }
}
```

- 时间复杂度 O(n) 每个字符串被访问了一次
- 空间复杂度 O(n)
