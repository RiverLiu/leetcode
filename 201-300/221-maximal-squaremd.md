# 221-最大正方形

tags: 动态规划
- https://leetcode-cn.com/problems/maximal-square/

最直接的思路是按照每行每列开始，逐渐增加节点判断是否是正方形，这种方法耗费时间长。

采用动态规划的思路，计算正方形的边长，从右下角向左上角的方向考虑，上面一个正方形的边长是最小的前一个，左一个，右一个中边长最小的加上自身边长的1. 对应的递推式为：

> dp[i][j]表示以第i行第j列为右下角所能构成的最大正方形边长, 则递推式为: 
> dp[i][j] = 1 + min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]);


```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if (matrix.length == 0) {
            return 0;
        }

        int maxVal = 0;
        int rowCount = matrix.length, columnCount = matrix[0].length;
        int[][] dp = new int[rowCount + 1][columnCount + 1]; 
        for (int row = 1; row <= rowCount; ++row) {
            for (int column = 1; column <= columnCount; ++column) {
               if (matrix[row-1][column-1] == '1') {
                   dp[row][column] = 1 + Math.min(dp[row-1][column-1], Math.min(dp[row-1][column], dp[row][column-1]));
                   maxVal = Math.max(dp[row][column], maxVal);
               }
            }
        }
        return maxVal * maxVal; 
    }
}
```