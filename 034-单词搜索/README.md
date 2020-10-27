# 题目

leetcode : [单词搜索](https://leetcode-cn.com/problems/word-search/)

## dfs + 回溯
```Java

class Solution {
        public boolean exist(char[][] board, String word) {
            int[][] director = {{1,0}, {-1,0}, {0,1}, {0,-1}};
            int[][] used = new int[board.length][board[0].length];
            for(int i=0;i<board.length;i++){
                for(int j=0;j<board[0].length;j++){
                    if(dfs(board, word, i, j, 0, director, used)){
                        return true;
                    }
                }
            }
            return false;

        }
        public boolean dfs(char[][] board, String word, int x, int y, int i, int[][] director, int[][] used){
            if(i==word.length()){
                return true;
            }
            if(x>=0 && x<board.length && y>=0 && y<board[0].length){
                if(used[x][y]==0 && board[x][y]==word.charAt(i)){
                    used[x][y] = 1;
                    for(int k=0;k<4;k++){
                        if(dfs(board, word, x+director[k][0], y+director[k][1], i+1, director, used)){
                            return true;
                        }
                    }
                    used[x][y] = 0;
                }
            }
            return false;
        }
        
    }
```
