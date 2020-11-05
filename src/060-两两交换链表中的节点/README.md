# 题目

leetcode : [两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

## 迭代 链表操作
```Java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode p = dummy;
        while(p.next!=null && p.next.next!=null){
            ListNode a = p.next;
            ListNode b = p.next.next;
            ListNode tail = b.next;
            p.next = b;
            b.next = a;
            a.next = tail;
            p = p.next.next;
        }
        return dummy.next;
    }
}
```
