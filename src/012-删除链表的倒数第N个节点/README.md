# 题目
leetcode : [删除链表的倒数第N个节点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

## 快慢指针
```Java

class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if(head==null){
            return null;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode fast = head;
        ListNode slow = dummy;
        while(n>0 && fast!=null){
            fast = fast.next;
            n--;
        }
        while(fast!=null){
            fast = fast.next;
            slow = slow.next;
        }
        
        slow.next = slow.next.next;
        return dummy.next;
    }
}
```
