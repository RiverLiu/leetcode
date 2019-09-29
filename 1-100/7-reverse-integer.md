# 整数反转

tags: Easy, String

- [题目链接](https://leetcode-.com/problems/reverse-integer/)
- [领扣链接](https://leetcode-cn.com/problems/reverse-integer/)

题目要求我们将一个整数进行反转，且保留符号，比如 `123` 反转之后变成 `321`. 题目难点在于反转的数据可能会溢出，有效的 32位有符号数据 $$[-2^{31}, 2^{31} - 1]$$，如果溢出了，返回结果为 0.

最先想到的一种方法，将数值转化为正数，然后判断每次加上个位数时，判断数值是否溢出，如果溢出，则返回 0

```java
class Solution {
    public int reverse(int x) {
        int tmp;
        int y = Math.abs(x);
        int num = 0;
        while (y > 0) {
            tmp = y % 10;
             y = y / 10;

            num = num * 10;
            if ((x > 0 && 2147483647 - num < tmp) || (x < 0 && 2147483647 - num < tmp - 1)) {
                return 0;
            }
            num = num + tmp;
            if (y > 0 && num > 214748365) {
                return 0;
            }
        }

        return x < 0 ? -num : num;
    }
}
```

上述方法，可以简化写法如下所示。

```java
class Solution {
    public int reverse(int x) {
        int tmp;
        int num = 0;
        int max = Integer.MAX_VALUE / 10;
        int min = Integer.MIN_VALUE / 10;
        while (x != 0) {
            tmp = x % 10;
            x = x / 10;
            if (num > max || (num == max && tmp > 7)) {
                return 0;
            }
            if (num < min || (num == min && tmp < -8)) {
                return 0;
            }
            num = num * 10 + tmp;
        }

        return x < 0 ? -num : num;
    }
}
```

网友提供了另外一种思路，如果数值溢出，那么求出的值对10整除，则会和原来的值不同，代码如下.

```java
  public int reverse(int x) {
    int result = 0;

    while (x != 0) {
        int tail = x % 10;
        int newResult = result * 10 + tail;
        if ((newResult - tail) / 10 != result) {
            return 0;
        }
        result = newResult;
        x = x / 10;
    }

    return result;
}
```
