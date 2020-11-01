# 题目

leetcode : [单词拆分](https://leetcode-cn.com/problems/word-break/)

##  简单dfs（超时）
```Java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        return dfs(s, wordDict, 0);

    }

    public boolean dfs(String s, List<String> wordDict, int start){
        if(start==s.length()){
            return true;
        }
        for(int i=0;i<wordDict.size();i++){
            String word = wordDict.get(i);
            int end = start+word.length();
            if(end<=s.length() && word.equals(s.substring(start, start+word.length()))){
                if(dfs(s, wordDict, start+word.length())){
                    return true;
                }
            }
        }
        return false;
    }
}
```

## 将dfs改写为dp
```Java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        boolean[] dp = new boolean[s.length()+1];  //长度为 i
        dp[0] = true;

        for(int i=0;i<s.length();i++){
            for(int j=0;j<wordDict.size();j++){
                String word = wordDict.get(j);
                if(i+1>=word.length()){
                    int start = i+1-word.length();
                    dp[i+1] = dp[start] && (word.equals(s.substring(start, i+1)));
                }
                if(dp[i+1]){
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```
