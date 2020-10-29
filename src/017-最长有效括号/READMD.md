# 题目

leetcode : [最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/submissions/)

有效括号
- 每一个左括号"("， 必定可以在他的右边找到一个右扩号")"与之相对应。
##  栈
- 用栈检查括号的有效性，在检查过程中记录长度。
```Java
    public int longestValidParentheses(String s) {
        int[] dp = new int[s.length()];
        int res = 0;
        for(int i=1;i<s.length();i++){
            if(s.charAt(i)=='('){
                continue;
            }
            if(s.charAt(i-1)=='('){
                dp[i] = i==1 ? 2 : dp[i-2] + 2;
            }
            else{
                if(i-dp[i-1]-1>=0 && s.charAt(i-dp[i-1]-1)=='('){
                    int tem = dp[i-1] + 2;
                    dp[i] = (i-dp[i-1]-2)>=0 ?  tem + dp[i-dp[i-1]-2] : tem;
                }
            }
            res = Math.max(res, dp[i]);
        }
        return res;
    }

```

## 动态规划
- dp[i] 以s[i]结尾的字符串的最长有效括号子串长度
```Java
    public int longestValidParentheses(String s) {
        int[] dp = new int[s.length()];
        int res = 0;
        for(int i=1;i<s.length();i++){
            if(s.charAt(i)=='('){
                continue;
            }
            if(s.charAt(i-1)=='('){
                dp[i] = i==1 ? 2 : dp[i-2] + 2;
            }
            else{
                if(i-dp[i-1]-1>=0 && s.charAt(i-dp[i-1]-1)=='('){
                    int tem = dp[i-1] + 2;
                    dp[i] = (i-dp[i-1]-2)>=0 ?  tem + dp[i-dp[i-1]-2] : tem; 
                }
            }
            res = Math.max(res, dp[i]);
        }
        return res;
    }
```
