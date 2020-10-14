# 题目
leetcode : [排序链表](https://leetcode-cn.com/problems/sort-list/)

# 归并排序
```Java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode sortList(ListNode head) {
        if(head==null || head.next==null){
            return head;
        }
        ListNode slow = head;
        ListNode fast = head.next;

        while(fast!=null && fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
        }

        fast = slow.next;
        slow.next = null;

        ListNode dummy = new ListNode(1);
        ListNode p = dummy;

        ListNode part1 = sortList(head);
        ListNode part2 = sortList(fast);

        while(part1!=null && part2!=null){
            if(part1.val<=part2.val){
                p.next = part1;
                part1 = part1.next;
            }
            else{
                p.next = part2;
                part2 = part2.next;
            }
            p = p.next;
        }
        if(part1!=null){
            p.next = part1;
        }
        if(part2!=null){
            p.next = part2;
        }
        return dummy.next;
    }
}
```
