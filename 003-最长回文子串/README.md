## 题目

leetcode : [003-最长回文字串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

## 解法一  中心扩展法
- 注意奇偶回文的问题
```Java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length()<2){
            return s;
        }
        int start = 0;
        int end = 0;
        int max_length = 0;
        for(int i=0;i<s.length();i++){
            int len = Math.max(expendAroundCenter(s, i, i), expendAroundCenter(s, i, i+1));
            if(len>max_length){
                max_length = len;
                start = i - (len - 1)/2;
                end = i + len/2;
            }
        }
        return s.substring(start, end+1);
    }

    public int expendAroundCenter(String s, int left, int right){
        while(left>=0 && right<s.length() && s.charAt(left)==s.charAt(right)){
            left--;
            right++;
        }
        return right - left - 1;
    }

}
```

## 解法二 马拉车
- 填充字符，将奇偶回文的情况都处理为奇回文
- 填充的时候记得用StringBuilder 而不是string
```Java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length()<2){
            return s;
        }
        //填充字符
        StringBuilder stringBuilder = new StringBuilder();
        stringBuilder.append("#");
        for(int i=0;i<s.length();i++){
            stringBuilder.append(s.charAt(i));
            stringBuilder.append("#");
        }
        s = stringBuilder.toString();

        int center = 0;
        int maxRigth = 0;
        int res = 0;
        int[] palindrome = new int[s.length()];
        for(int i=0;i<s.length();i++){
            int mrrior = 2*center - i;
            if(i>=maxRigth||(i+palindrome[mrrior])>=maxRigth){
                maxRigth = expendMaxRight(s, i);
                center = i;
                palindrome[i] = maxRigth - i + 1;
            }
            else{
                palindrome[i] = palindrome[mrrior];
            }
            res = Math.max(res, palindrome[i]);
        }

        for(int i=0;i<s.length();i++){
            if(palindrome[i]==res){
                s = s.substring(i-res+1, i+res);
                s = s.replace("#", "");
                break;
            }
        }
        return s;

    }

    public int expendMaxRight(String s, int i){
        int left = i-1;
        int right = i+1;
        while(left>=0 && right<s.length() && s.charAt(left)==s.charAt(right)){
            left--;
            right++;
        }
        return right-1;
    }
}
```


