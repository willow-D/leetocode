# 题目

leetcode : [柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)

## 单调栈 + 哨兵
```Java
class Solution {
    public int largestRectangleArea(int[] heights) {
        if(heights.length==0){
            return 0;
        }
        int[] newHeights = new int[heights.length+2];
        for(int i=0;i<heights.length;i++){
            newHeights[i+1] = heights[i];
        }
        Stack<Integer> stack = new Stack<>();
        int res = 0;
        for(int i=0;i<newHeights.length;i++){
            while(!stack.empty() && newHeights[i]<newHeights[stack.peek()]){
                int cur = stack.pop();
                int l = stack.peek();
                int r = i;
                res = Math.max(res, (r - l - 1) * newHeights[cur]);
            }
            stack.add(i);
        }

        return res;
    }
}

```
