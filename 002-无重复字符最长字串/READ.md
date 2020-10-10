## 题目

leetcode : [002-无重复字符最长字串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

## 解法一
- 用一个map记录下最新出现的字符的下标
- 维护一个动态区间
 ```Java
 class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s.length()==0){
            return 0;
        }
        Map<Character, Integer> map = new HashMap<>();
        int res = 1;
        int left = 0;

        for(int r=0;r<s.length();r++){
            if(map.containsKey(s.charAt(r))){
                left = Math.max(left, map.get(s.charAt(r))+1);
            }
            map.put(s.charAt(r), r);
            res = Math.max(res, r-left+1);
        }
        return res;
    }

}
```
