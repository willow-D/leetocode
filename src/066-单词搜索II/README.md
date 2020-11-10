# 题目

leetcode : [单词搜索II](https://leetcode-cn.com/problems/word-search-ii/)

## dfs + 前缀树
```Java
import java.util.HashSet;
import java.util.LinkedList;
import java.util.List;
import java.util.Set;

public class Solution {

    class Trie{
        boolean isEnd = false;
        public Trie[] next = new Trie[26];

        public void insert(String words){
            Trie root = this;
            char[] word = words.toCharArray();
            for(char c:word){
                if(root.next[c-'a']==null){
                    root.next[c-'a'] = new Trie();
                }
                root = root.next[c-'a'];
            }
            root.isEnd = true;
        }

        public boolean startWith(String words){
            Trie root = this;
            char[] word = words.toCharArray();
            for(char c : word){
                if(root.next[c - 'a']==null){
                    return false;
                }
                root = root.next[c - 'a'];
            }
            return true;
        }
        public boolean search(String words){
            Trie root = this;
            char[] word = words.toCharArray();
            for(char c : word){
                if(root.next[c - 'a']==null){
                    return false;
                }
                root = root.next[c - 'a'];
            }
            return root.isEnd;
        }

    }

    public List<String> findWords(char[][] board, String[] words) {
        Trie trie = new Trie();
        for(String s : words){
            trie.insert(s);
        }
        Set<String> res = new HashSet<>();
        StringBuffer stringBuffer = new StringBuffer();
        int[][] direct = {{1,0}, {-1,0}, {0,1},{0,-1}};
        boolean[][] used = new boolean[board.length][board[0].length];
        for(int i=0;i<board.length;i++){
            for(int j=0;j<board[0].length;j++){
                dfs(res, stringBuffer, board, used, trie, i,j, direct);
            }
        }
        List<String> r = new LinkedList<>(res);
        return r;

    }

    public void dfs(Set<String> res, StringBuffer stringBuffer, char[][] board, boolean[][] used, Trie trie, int x, int y, int[][] direct){
        if(x>=0 && x<board.length && y>=0 && y<board[0].length){
            if(used[x][y]){
                return;
            }
            stringBuffer.append(board[x][y]);
            String s = stringBuffer.toString();
            if(trie.startWith(s)){
                if(trie.search(s)){
                    res.add(s);
                }
                used[x][y] = true;
                for(int i=0;i<4;i++){
                    dfs(res, stringBuffer, board, used, trie, x+direct[i][0], y+direct[i][1], direct);
                }
                used[x][y] = false;
            }
            stringBuffer.deleteCharAt(stringBuffer.length()-1);
        }
    }
}

```
