# median-of-two-sorted-arrays 寻找两个有序数组的中位数

- [题目链接](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [领扣链接](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)
- [tag] Hard, Array, Binary Search, Divide and Conquer

我提交的解法

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int count = nums1.length + nums2.length;
        int mi = 0;
        int ni = 0;
        int midVal = 0;
        int mid = (count - 1) / 2;
        while (mi + ni <= mid) {
            if (mi == nums1.length) {
                midVal = nums2[mid - nums1.length];
                break;
            }
            if (ni == nums2.length) {
                midVal = nums1[mid - nums2.length];
                break;
            }
            if (nums1[mi] >= nums2[ni]) {
                midVal = nums2[ni];
                ++ni;
            } else {
                midVal = nums1[mi];
                ++mi;
            }
        }
        
        if (count % 2 != 0) {
            return (double)midVal;
        } else {
            if (mi == nums1.length) {
                return (midVal +  nums2[mid + 1 - nums1.length]) / 2.0; 
            } else if (ni == nums2.length) {
                return (midVal + nums1[mid + 1 - nums2.length]) / 2.0;
            } else {
                if (nums1[mi] >= nums2[ni]) {
                    return (midVal + nums2[ni]) / 2.0;
                } else {
                    return (midVal + nums1[mi]) / 2.0;
                }
            }
        }
    }
}
```

官方解法

```java
class Solution {
    public double findMedianSortedArrays(int[] A, int[] B) {
        int m = A.length;
        int n = B.length;
        if (m > n) { // to ensure m<=n
            int[] temp = A; A = B; B = temp;
            int tmp = m; m = n; n = tmp;
        }
        int iMin = 0, iMax = m, halfLen = (m + n + 1) / 2;
        while (iMin <= iMax) {
            int i = (iMin + iMax) / 2;
            int j = halfLen - i;
            if (i < iMax && B[j-1] > A[i]){
                iMin = i + 1; // i is too small
            }
            else if (i > iMin && A[i-1] > B[j]) {
                iMax = i - 1; // i is too big
            }
            else { // i is perfect
                int maxLeft = 0;
                if (i == 0) { maxLeft = B[j-1]; }
                else if (j == 0) { maxLeft = A[i-1]; }
                else { maxLeft = Math.max(A[i-1], B[j-1]); }
                if ( (m + n) % 2 == 1 ) { return maxLeft; }

                int minRight = 0;
                if (i == m) { minRight = B[j]; }
                else if (j == n) { minRight = A[i]; }
                else { minRight = Math.min(B[j], A[i]); }

                return (maxLeft + minRight) / 2.0;
            }
        }
        return 0.0;
    }
}
```
