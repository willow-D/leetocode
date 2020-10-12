# 题目
leetcode : [004-Z字形变换](https://leetcode-cn.com/problems/zigzag-conversion/)

## 思路，找规律
-  首尾两行 index + (numRows-1)*2
- 中间的是 index + (numRows-1)*2 - i*2 , index + i*2

## 解法一
```
class Solution {
    public String convert(String s, int numRows) {
        if(s.length()<2){
            return s;
        }
        if(numRows==1){
            return s;
        }
        int l = (numRows - 1)*2;

        StringBuilder stringBuilder = new StringBuilder();
        for(int i=0;i<numRows;i++){
            if(i==0||i==numRows-1){
                int index = i;
                while(index<s.length()){
                    stringBuilder.append(s.charAt(index));
                    index+=l;
                }
            }
            else{
                int l2 = i*2;
                int l1 = l- l2 ;
                if(l1==l2){
                    int index = i;
                    while(index<s.length()){
                        stringBuilder.append(s.charAt(index));
                        index+=l1;
                    }
                }
                else{
                    int flag = 0;
                    int index = i;
                    while(index<s.length()){
                        stringBuilder.append(s.charAt(index));
                        index+= flag%2==0 ? l1 : l2;
                        flag++;
                    }
                }
            }

        }
        return stringBuilder.toString();
    }
}
```

## 解法二 同样的思路，代码经过优化
```
class Solution {
    public String convert(String s, int numRows) {
        if(numRows<2){
            return s;
        }
        
        int l = (numRows - 1)*2;
        StringBuilder stringBuilder = new StringBuilder();
        for(int i=0;i<numRows;i++){
            int add = i*2;
            int index = i;
            while(index<s.length()){
                stringBuilder.append(s.charAt(index));
                add = l - add;  // 这里是个小技巧
                index += i==0||i==numRows-1 ? l : add;  
            }
        }
        return stringBuilder.toString();
    }
}
```
