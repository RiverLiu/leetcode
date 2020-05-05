# 229-求众数 II

tags: 数组
- https://leetcode-cn.com/problems/majority-element-ii/

>【笔记】摩尔投票法。该算法用于1/2情况，它说：“在任何数组中，出现次数大于该数组长度一半的值只能有一个。”
>那么，改进一下用于1/3。可以着么说：“在任何数组中，出现次数大于该数组长度1/3的值最多只有两个。”
>于是，需要定义两个变量。空间复杂度为O(1)。
>摩尔投票法：https://mabusyao.iteye.com/blog/2223195
>算法1/3改进：https://blog.csdn.net/weixin_42768679/article/details/81567231

使用改进的摩尔投票法.
```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        int x = 0, y = 0, cx = 0, cy = 0;
        for (int num : nums) {
            if ((cx == 0 || x == num) && num != y) {
                x = num;
                ++cx;
            } else if (cy == 0 || y == num) {
                y = num;
                ++cy;
            } else {
                --cx;
                --cy;
            }
        }

        cx = 0; cy = 0;
        for (int num : nums) {
            if (num == x) {
                ++cx;
            } else if (num == y) {
                ++cy;
            }
        }
        List<Integer> elements = new ArrayList<>(2);
        if (cx > nums.length / 3) {
            elements.add(x);
        }
        if (cy > nums.length / 3) {
            elements.add(y);
        }
        return elements;
    }
}
```
