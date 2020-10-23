# 题目

leetcode : [合并区间](https://leetcode-cn.com/problems/merge-intervals/)

## 自定义排序
```Java
class Solution {
    public int[][] merge(int[][] intervals) {
        if(intervals.length<2){
            return intervals;
        }
        Arrays.sort(intervals, ((int[] o1, int[]o2) -> {
            return o1[0] - o2[0];
        }));

        List<int[]> res = new LinkedList<>();
        int start=intervals[0][0];
        int end = intervals[0][1];

        for(int i=1;i<intervals.length;i++){
            if(intervals[i][0]>end){
                res.add(new int[]{start, end});
                start = intervals[i][0];
                end = intervals[i][1];
            }
            end = Math.max(end, intervals[i][1]);
            if(i==intervals.length-1){
                res.add(new int[]{start, end});
            }
        }
        int[][] re = new int[res.size()][2];
        res.toArray(re);
        
        return re;
    }
}
```
