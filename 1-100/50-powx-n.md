# 50-Pow(x, n)

tags: 数学，二分查找
- https://leetcode-cn.com/problems/powx-n/

使用常规直接乘的方法，会造成超时的问题，使用二分法将分开计算。

>使用折半计算，每次把n缩小一半，这样n最终会缩小到0，任何数的0次方都为1，这时候我们再往回乘，如果此时n是偶数，直接把上次递归得到的值算个平方返回即可，如果是奇数，则还需要乘上个x的值。还有一点需要引起我们的注意的是n有可能为负数，对于n是负数的情况，我们可以先用其绝对值计算出一个结果再取其倒数即可。我们让i初始化为n，然后看i是否是2的倍数，是的话x乘以自己，否则res乘以x，i每次循环缩小一半，直到为0停止循环。最后看n的正负，如果为负，返回其倒数。

```java
class Solution {
    public double myPow(double x, int n) {
        double val = 1.0;
        for (int i = n; i != 0; i /= 2) {
            if (i % 2 != 0) {
                val *= x;
            }
            x *= x;
        }
    
        return n > 0 ? val : 1/val;
    }
}
```

递归分治的形式代码，参考极客时间课程: https://time.geekbang.org/course/detail/100019701-42711

```python
class Solution(object):
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        if not n:
            return 1
        if n < 0:
            return 1 / self.myPow(x, -n)
        if n % 2 == 0:
            return self.myPow(x*x, n / 2)
        else:
            return self.myPow(x*x, n / 2) * x
```

如果改成非递归的形式:

```python
class Solution(object):
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        if n < 0:
            x = 1 / x
            n = -n
        
        val = 1
        while n != 0:
            if n % 2 != 0:
                val *= x
            x *= x
            n = n // 2
        return val
```

使用位运算

```python
class Solution(object):
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        if n < 0:
            x = 1 / x
            n = -n
        
        val = 1
        while n != 0:
            if n & 1:
                val *= x
            x *= x
            n >>= 1
        return val

```
