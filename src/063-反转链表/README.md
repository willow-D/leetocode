# 题目

leetcode : [反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

## 递归
```Java
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head==null || head.next==null){
            return head;
        }
        ListNode next = head.next;
        head.next = null;
        ListNode res = reverseList(next);
        next.next = head;
        return res;
    }
}
```

## 迭代
```Java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode p = head;
        ListNode pre = null;
        while(p!=null){
            ListNode next = p.next;
            p.next = pre;
            pre = p;
            p = next;
        }
        return pre;
    }
}
```
