# 题目

leetcode : [课程表II](https://leetcode-cn.com/problems/course-schedule-ii/)

## 拓扑排序
```Java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> edges = new LinkedList<List<Integer>>();
        int[] inCnt = new int[numCourses];
        int[] res = new int[numCourses];
        int index = 0;

        for(int i=0;i<numCourses;i++){
            edges.add(new LinkedList<Integer>());
        }
        for(int[] info : prerequisites){
            inCnt[info[0]]++;
            edges.get(info[1]).add(info[0]);
        }

        Queue<List<Integer>> queue = new LinkedList<List<Integer>>();
        for(int i=0;i<inCnt.length;i++){
            if(inCnt[i]==0){
                res[index++] = i;
                queue.offer(edges.get(i));
            }
        }

        while(!queue.isEmpty()){
            List<Integer> edge = queue.poll();
            for(Integer i: edge){
                inCnt[i]--;
                if(inCnt[i]==0){
                    queue.offer(edges.get(i));
                    res[index++] = i;
                }
            }
        }
        return index==numCourses ? res : new int[0];
    }
}
```
