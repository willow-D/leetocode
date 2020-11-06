# 题目
leetcode : [课程表](https://leetcode-cn.com/problems/course-schedule/)


## 图的排序
- 邻接矩阵：容易判断两点是否存在边，对边的增加、删除都方便。空间效率不高，判断点的出度和入度不方便
- 邻接表：入度不好求，额外开一个入度数组比较好。判断两点是否有边比较麻烦。
## 拓扑排序
-推荐从入度的角度展开
找到所有入度为零的点，然后删除他们的出度。重复，直到不存在入度为零的点。

```Java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> edges = new LinkedList<List<Integer>>();
        int[] in = new int[numCourses];

        for(int i=0;i<numCourses;i++){
            edges.add(new LinkedList<Integer>());
        }
        for(int[] info : prerequisites){
            edges.get(info[0]).add(info[1]);
            in[info[1]]++;
        }
        
        int visited = 0;
        Queue<List<Integer>> queue = new LinkedList<List<Integer>>();
        for(int i=0;i<in.length;i++){
            if(in[i]==0){
                queue.offer(edges.get(i));
                visited++;
            }
        }

        while(!queue.isEmpty()){
            List<Integer> edge = queue.poll();
            for(Integer i:edge){
                in[i]--;
                if(in[i]==0){
                    queue.offer(edges.get(i));
                    visited++;
                }
            }
        }
        return visited==numCourses;
    }
}
```
