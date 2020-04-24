# 整数转罗马数字

tags: Medium, Math, String

- [题目链接](https://leetcode.com/problems/integer-to-roman)
- [领扣链接](https://leetcode-cn.com/problems/integer-to-roman)

按照数字大小处理的方法。

```java
class Solution {
    public String intToRoman(int num) {

        char c;
        int cnt;
        int tmp;
        String s = "";

        if ((tmp = num / 1000) > 0) {
            s = addRoman(s, tmp, "M");
            num %= 1000;
        }
        if (num >= 900) {
            s += "CM";
            num -= 900;
        } else  if (num >= 500) {
            s += "D";
            num -= 500;
        } else if (num >= 400) {
            s += "CD";
            num -= 400;
        }

        if ((tmp = num / 100) > 0) {
            s = addRoman(s, tmp, "C");
            num %= 100;
        }
        if (num >= 90) {
            s += "XC";
            num -= 90;
        } else if (num >= 50) {
            s += "L";
            num -= 50;
        } else if (num >= 40) {
            s += "XL";
            num -= 40;
        }

        if ((tmp = num / 10) > 0) {
            s = addRoman(s, tmp, "X");
            num %= 10;
        }
        if (num >= 9) {
            s += "IX";
            num -= 9;
        } else if (num >= 5) {
            s += "V";
            num -= 5;
        } else if (num >= 4) {
            s += "IV";
            num -= 4;
        }
        s = addRoman(s, num, "I");

        return s;
    }

    public String addRoman(String s, int count, String c) {
        while (count > 0) {
            s += c;
            --count;
        }
        return s;
    }
}
```

一种简化版本的写法，精心构造的字符串。

```c++
class Solution {
public:
    string intToRoman(int num) {
        static const string s[4][10] = {
          {"","I","II","III","IV","V","VI","VII","VIII","IX"},
          {"","X","XX","XXX","XL","L","LX","LXX","LXXX","XC"},
          {"","C","CC","CCC","CD","D","DC","DCC","DCCC","CM"},
          {"","M","MM","MMM"},
        };

        return s[3][num/1000%10] + s[2][num/100%10] + s[1][num/10%10] + s[0][num%10];
    }
};
```

另外一种迭代的写法

```java
public static String intToRoman(int num){
    if (num < 1 || num > 3999) return "";

    StringBuilder result = new StringBuilder();

    String[] roman = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
    int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1 };

    int i = 0;
    //iterate until the number becomes zero, NO NEED to go until the last element in roman array
    while (num >0) {
      while ( num >= values[i]) {
        num -= values[i];
        result.append(roman[i]);
      }
      i++;
    }
    return result.toString();
}
```
