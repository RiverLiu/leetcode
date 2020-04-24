# 罗马数字转整数

tags: Easy, Math, String

- [题目链接](https://leetcode.com/problems/roman-to-integer)
- [领扣链接](https://leetcode.com/problems/roman-to-integer)

```java
class Solution {
    public int romanToInt(String s) {
    String[] roman = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
          int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1 };

          int num = 0;
          int idx = 0;
          for (int i = 0; i < s.length();) {
              if (s.startsWith(roman[idx], i)) {
                  num += values[idx];
                  i += roman[idx].length();
              } else {
                  ++idx;
              }
          }

          return num;
    }
}
```
