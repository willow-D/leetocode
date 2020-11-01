# 题目

leetcode : [环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

## 快慢指针
- 如果有环，快慢指针会相遇
- 当相遇时，快指针从头开始一步一步的走，当再次相遇时，就是入环节点

```Java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head==null){
            return false;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while(fast!=null && fast.next!=null){
            fast = fast.next.next;
            slow = slow.next;
            if(fast==slow){
                return true;
            }
        }
        return false;
    }
}
```
