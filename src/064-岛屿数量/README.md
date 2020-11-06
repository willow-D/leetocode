#题目

leetcode : [岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

## dfs
```Java
class Solution {
    public int numIslands(char[][] grid) {
        boolean[][] used = new boolean[grid.length][grid[0].length];
        int [][] direct = {{0,1}, {0,-1}, {1,0}, {-1,0}};
        int res = 0;
        for(int i=0;i<grid.length;i++){
            for(int j=0;j<grid[0].length;j++){
                if(grid[i][j]=='1' && used[i][j]==false){
                    res++;
                    dfs(grid, used, direct, i, j);
                }
            }
        }
        return res;

    }

    public void dfs(char[][] grid, boolean[][] used, int[][] direct, int i, int j){
        if(i>=0 && i<grid.length && j>=0 && j<grid[0].length){
            if(grid[i][j]=='1' && used[i][j]==false){
                used[i][j] = true;
                for(int k=0;k<4;k++){
                    dfs(grid, used, direct, i+direct[k][0], j+direct[k][1]);
                }
            }
        }
    }
}
```
