# 120-三角形最小路径和

tags: 动态规划
- https://leetcode-cn.com/problems/triangle/

解法一： 采用自顶而下的解法，走到下一步时，选择上一步最小的路径，然后走到最底层时，寻找最短的路径值。

其中，有一个需要注意，每一行，前面那个和最后一个，需要特殊处理。

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        if (triangle == null || triangle.size() == 0) {
            return 0;
        }
    
        int rowCount = triangle.size();
        int paths[] = new int[rowCount];
        paths[0] = triangle.get(0).get(0);
        
        int min = 0;
        for (int row = 1; row < rowCount; ++row) {
            for (int column = row; column >= 0; --column) {
                min = column == row ?  min = paths[row - 1] : (column == 0 ? paths[0] : Math.min(paths[column - 1], paths[column]));
                paths[column] = triangle.get(row).get(column) + min;
            }
        }

        min = paths[0];
        for (int i = 1; i < rowCount; ++i) {
            if (min > paths[i]) {
                min = paths[i];
            }
        }
        return min;
    }
}
```

解法二：采用自底而上的DP解法。思想与上一个相同，初始状态为最后一行的值，然后向上查找最短路径，最终到最顶端的路径为最短路径。

```java

class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        if (triangle == null || triangle.size() == 0) {
            return 0;
        }

        int rowCount = triangle.size();
        int paths[] = new int[rowCount];
        List<Integer> last = triangle.get(rowCount - 1);
        for (int i = 0; i < rowCount; ++i) {
            paths[i] = last.get(i);
        }

        for (int i = rowCount - 2; i >= 0; --i) {
            for (int j = 0; j <= i; ++j) {
                paths[j] = triangle.get(i).get(j) + Math.min(paths[j], paths[j + 1]);
            }
        }
        return paths[0];
    }

}
```