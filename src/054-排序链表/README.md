# 题目

leetcode : [排序链表](https://leetcode-cn.com/problems/sort-list/)

## 归并排序
```Java
class Solution {
    public ListNode sortList(ListNode head) {
        if(head==null || head.next==null){
            return head;
        }

        ListNode slow = head;
        ListNode fast = head.next;
        while(fast!=null && fast.next!=null){
            fast = fast.next.next;
            slow = slow.next;
        }
        fast = slow.next;
        slow.next = null;

        ListNode left = sortList(head);
        ListNode right = sortList(fast);

        ListNode dummy = new ListNode();
        ListNode p = dummy;
        while(left!=null && right!=null){
            if(left.val<right.val){
                p.next = left;
                left = left.next;
            }
            else{
                p.next = right;
                right = right.next;
            }
            p = p.next;
        }
        if(left!=null){
            p.next = left;
        }
        if(right!=null){
            p.next = right;
        }
        return dummy.next;
    }
}
```
