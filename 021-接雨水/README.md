# 题目

leetcode : [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/submissions/)

## 数组处理
- 先把数组划分称为一个个的小池子，然后减去池内石柱的面积，得到雨水的面积
- 先固定一根石柱为左边，然后寻找第一根比他大的石柱，作为右边，这两根石柱组成一个小水池。
- 左边石柱长度不能为0
- 当右边石柱都比较小的时候，反转一下，不影响
```Java
    class Solution {

        public int trap(int[] height) {
            return trap(height, 0, 0);
        }

        public int trap(int[] height, int start, int res){
            if(start>=height.length-1){
                return res;
            }
            int left = height[start];
            while(start<height.length){
                if(height[start]==0){
                    start++;
                    continue;
                }
                left = height[start];
                break;
            }

            int end ;
            boolean flag = false;
            for(end=start+1;end<height.length;end++){
                if(height[end]>=left){
                    right = height[end];
                    flag = true;
                    break;
                }
            }
            if(!flag){
                reverse(height, start);
                return trap(height, start, res);
            }
            int area = left*(end-start-1);
            for(int i=start+1;i<end;i++){
                area-=height[i];
            }
            return trap(height, end, res+area);
        }

        public void swap(int[] height, int i, int j){
            int tem = height[i];
            height[i] = height[j];
            height[j] = tem;
        }

        public void reverse(int[] height, int i){
            int j = height.length-1;
            while(i<=j){
                swap(height, i, j);
                i++;
                j--;
            }
        }

    }
```
