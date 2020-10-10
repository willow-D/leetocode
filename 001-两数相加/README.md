# 一级标题

## 题目

leetcode ：[001-两数之和](https://leetcode-cn.com/problems/add-two-numbers/)

## 解法一
遍历一遍链表，将其处理成数字相加，然后在转换成链表。
但是数值太大，会溢出，一开始没注意这个问题。

## 解法二
# 直接模拟相加
- 两个链表首先要对齐，使得二者长度相等
- 注意最后一位进位的问题

```
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        align(l1,l2);

        ListNode dummy = new ListNode(0);
        ListNode p = dummy;
        int carry = 0;
        while(l1!=null){
            int sum = l1.val+l2.val+carry;
            if(sum>=10){
                carry = 1;
                sum%=10;
            }
            else{
                carry = 0;
            }
            p.next = new ListNode(sum);
            p = p.next;
            l1 = l1.next;
            l2 = l2.next;
        }

        if(carry==1){
            p.next = new ListNode(1);
        }
        return dummy.next;

    }

    public void align(ListNode l1, ListNode l2){ //确定l1 l2是非空的
        while(l1.next!=null||l2.next!=null){
            if(l1.next==null){
                l1.next = new ListNode(0);
            }
            if(l2.next==null){
                l2.next = new ListNode(0);
            }
            l1 = l1.next;
            l2 = l2.next;
        }
        return;
    }
}

```

