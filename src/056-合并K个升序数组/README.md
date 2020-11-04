# 题目
leetcode : [合并K个升序数组](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

## K路合并
```Java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode dummy = new ListNode();
        ListNode p = dummy;
        if(lists.length==0){
            return dummy.next;
        }
        while(true){
            ListNode minNode = new ListNode(Integer.MAX_VALUE);
            int minIndex = -1;
            boolean end = true;
            for(int i=0;i<lists.length;i++){
                if(lists[i]==null){
                    continue;
                }
                end = false;
                if(lists[i].val<=minNode.val){
                    minNode = lists[i];
                    minIndex = i;
                }
            }
            if(end){
                break;
            }            
            p.next = minNode;
            p = p.next;
            lists[minIndex] = lists[minIndex].next;
        }
        return dummy.next;
    }
}
```
## 用优先队列进行优化
- 在取最小节点的过程中，存在大量重复遍历，开一个优先队列将他们存起来。 空间换时间
- 优先队列的初始化，传入比较器
```Java

class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode dummy = new ListNode();
        ListNode p = dummy;
        if(lists.length==0){
            return dummy.next;
        }
        Queue<ListNode> priorityQueue = new PriorityQueue<>((n1, n2)-> n1.val - n2.val);
        for(ListNode node : lists){
            if(node!=null){
                priorityQueue.offer(node);
            }    
        }
        while(!priorityQueue.isEmpty()){
            ListNode node = priorityQueue.poll();
            p.next = node;
            p = p.next;
            if(node.next!=null){
                priorityQueue.offer(node.next);
            }  
        }
        return dummy.next;
    }
}
```
