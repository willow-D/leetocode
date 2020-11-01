#题目

leetcode : [只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

## 异或的性质
- 0 和任何数异或都还是数本身
- 两个相同的数异或等于0

```Java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for(int n:nums){
            res^=n;
        }
        return res;
    }
}
```
