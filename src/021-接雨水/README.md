# 题目

leetcode : [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/submissions/)

## 列的角度
-向左向右找到能包围自己的最大柱子长度，然后减去自己的长度。

```Java
class Solution {
    public int trap(int[] height) {
        if(height.length<3){
            return 0;
        }
        int[] maxLeft = new int[height.length];
        int[] maxRigth = new int[height.length];

        maxLeft[0] = height[0];
        for(int i=1;i<height.length;i++){
            maxLeft[i] = Math.max(height[i], maxLeft[i-1]);
        }
        maxRigth[height.length-1] = height[height.length-1];
        for(int i=height.length-2;i>=0;i--){
            maxRigth[i] = Math.max(height[i], maxRigth[i+1]);
        }

        int res = 0;
        for(int i=1;i<height.length-1;i++){
            res+=(Math.min(maxLeft[i], maxRigth[i]) - height[i]);
        }
        return res;

    }
}
```

## 行的角度 （单调栈）
- 维护一个单调递减栈
- 减去底的高度
- 单调栈模板
```Java
class Solution {
    public int trap(int[] height) {
        if(height.length<3){
            return 0;
        }
        Stack<Integer> stack = new Stack<>();
        int res = 0;
        for(int i=0;i<height.length;i++){
            while(!stack.empty() && height[i]>height[stack.peek()]){
                int cur = stack.pop();
                if(stack.empty()){
                    break;
                }
                int l = stack.peek();
                int r = i;
                res+=(Math.min(height[l], height[r])-height[cur])*(r-l-1);    
            }
            stack.add(i);
        }
        return res;
    }   
}

```



