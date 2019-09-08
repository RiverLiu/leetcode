# Z 字形变换

https://leetcode.com/problems/zigzag-conversion/submissions/


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

- 时间复杂度 O(n^2)
- 空间复杂度 O(n)