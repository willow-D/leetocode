# 题目

leetcode : [旋转数组](https://leetcode-cn.com/problems/rotate-image/)

 
- 上下颠倒相当于旋转了180度
- 转置相当于旋转了270 
- 旋转450度相当于旋转了90

```Java
class Solution {
    public void rotate(int[][] matrix) {
        
        topBottom(matrix);
        transposition(matrix);

    }
    public void transposition(int[][] matrix){
        for(int i=0;i<matrix.length;i++){
            for(int j=i;j<matrix[0].length;j++){
                int tem = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tem;
            }
        }
    }

    public void topBottom(int[][] matrix){
        for(int j=0;j<matrix[0].length;j++){
            int top = 0;
            int bottom = matrix.length-1;
            while(top<=bottom){
                int tem = matrix[top][j];
                matrix[top][j] = matrix[bottom][j];
                matrix[bottom][j] = tem;
                top++;
                bottom--;
            }
        }
    }
}
```
