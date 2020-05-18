# 210-课程表 II

tags: 深度优先搜索，广度优先搜索，图，拓扑排序
- https://leetcode-cn.com/problems/course-schedule-ii/


解法一：拓扑排序，整体思想为：按照图计算依赖课程的入度，先学习入度为0的课程，然后调整被依赖课程的入度，如果入度变为0，课程可以学习

```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        int[] degree = new int[numCourses];
        for (int i = 0; i < prerequisites.length; ++i) {
            // 计算课程节点的入度
            degree[prerequisites[i][0]]++;
        }

        int idx = 0, cur;
        int res[] = new int[numCourses];
        for (int i = 0; i < numCourses; ++i) {
            // 如果入度为0，则可以学习课程
            if (degree[i] == 0) {
                res[idx++] = i;

                // 使用 cur 表示当前课程的索引记录
                // idx 表示下一个学习课程的索引记录
                cur = idx - 1;
                while (cur < idx) {
                    // 将依赖于 i 课程的入度减1，并检测入度是否变成0，
                    // 如果入度为0 且是已经遍历过的课程，可以学习
                    // 同时检测该门课的依赖课程的入度，是否可以学习
                    for (int j = 0; j < prerequisites.length; ++j) {
                        if (prerequisites[j][1] == res[cur]) {
                            int k = prerequisites[j][0];
                            --degree[k];
                            if (degree[k] == 0 && k < i) {
                                res[idx++] = k;
                            }
                        }
                    }
                    ++cur;
                }
            }
        }

        // 如果学习的课程和课程总数不一致（依赖课程存在环），按照题目要求返回空数组
        return idx == numCourses ? res : new int[0];
    }
}
```
