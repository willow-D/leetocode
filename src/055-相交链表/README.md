# 题目

leetcode : [相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

## 对齐长度

```Java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        int cntA = 0;
        int cntB = 0;
        ListNode p = headA;
        while(p!=null){
            cntA++;
            p = p.next;
        }
        p = headB;
        while(p!=null){
            cntB++;
            p = p.next;
        }
        if(cntA>cntB){
            int cnt = cntA - cntB;
            while(cnt>0){
                headA = headA.next;
                cnt--;
            }
        }
        if(cntA<cntB){
            int cnt = cntB - cntA;
            while(cnt>0){
                headB = headB.next;
                cnt--;
            }
        }

        while(headA!=null){
            if(headA==headB){
                return headA;
            }
            headA = headA.next;
            headB = headB.next;
        }
        return null;
    }
}
```

## 优化后
```Java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode pA = headA;
        ListNode pB = headB;

        while(pA!=pB){
            pA = pA==null ? headB : pA.next;
            pB = pB==null ? headA : pB.next;
        }
        return pB;
    }
}
```
