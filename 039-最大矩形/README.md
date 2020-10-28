# 题目

leetcode : [最大矩形](https://leetcode-cn.com/problems/maximal-rectangle/)

## 转化为柱状图中的最大矩形
- 时间复杂度O(NM)
```Java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        int res = 0;
        if (matrix.length == 0) {
            return res;
        }
        int[] heights = new int[matrix.length + 2];
        for (int j = matrix[0].length-1; j >=0; j--) {
            for (int i = 0; i < matrix.length; i++) {
                heights[i+1] = matrix[i][j]=='1' ? heights[i+1]+1 : 0;
            }
            res = Math.max(res, merge(heights));
        }
        return res;
    }
    
    public int merge(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int res = 0;
        for (int i = 0; i < heights.length; i++) {
            while (!stack.empty() && heights[stack.peek()] > heights[i]) {
                int height = heights[stack.pop()];
                int l = stack.peek();
                int r = i;
                res = Math.max(res, (r - l - 1) * height);
            }
            stack.add(i);
        }
        return res;
    }
}
```

## dp
- 时间复杂度 O(NMK)

```JAVA
class Solution {
        public int maximalRectangle(char[][] matrix) {
            int res = 0;
            if(matrix.length==0){
                return res;
            }
            int[][][] dp = new int[matrix.length][matrix[0].length][2];  // 长、 宽

            for(int i=0;i<matrix.length;i++){
                for(int j=0;j<matrix[0].length;j++){
                    if(matrix[i][j]!='1'){
                        continue;
                    }
                    if(i==0 && j==0){
                        dp[i][j] = new int[]{1, 1};
                        res=1;
                    }
                    else if(i==0){
                        dp[i][j] = new int[]{1,dp[i][j-1][1] + 1};
                        res = Math.max(res,dp[i][j][1]);
                    }
                    else if(j==0){
                        dp[i][j] = new int[]{dp[i-1][j][0]+1, 1};
                        res = Math.max(res, dp[i][j][0]);
                    }
                    else{
                        dp[i][j] = new int[]{dp[i-1][j][0]+1, dp[i][j-1][1]+1};
                        int row = dp[i][j][0];
                        int minCol = dp[i][j][1];
                        for(int k=0;k<row;k++){
                            minCol = Math.min(minCol, dp[i-k][j][1]);
                            res = Math.max(res, minCol*(k+1));
                        }
                    }
                }
            }
            return res;
        }

}
```
