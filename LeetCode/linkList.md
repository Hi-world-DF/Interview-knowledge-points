# 链表
* [1. IntersectionOfTwoLinkedLists (找出两个链表的交点)]()

## ListNode类的定义
``` java
class ListNode {
     int val;
     ListNode next;
     ListNode(int x) {
         val = x;
         next = null;
     }
}
```

## 1. IntersectionOfTwoLinkedLists (找出两个链表的交点)
问题描述：[LeedCode](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)   
解决代码：
``` java
/**
 * 数据结构：链表
 * leetcode：https://leetcode-cn.com/problems/intersection-of-two-linked-lists/
 * 找出两个链表的交点
 * */
public class IntersectionOfTwoLinkedLists {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode listA = headA;
        ListNode listB = headB;
        while(listA != listB){
            listA = (listA == null)?headB:listA.next;
            listB = (listB == null)?headA:listB.next;
        }
        return listA;
    }
}
```
## 2. MergeTwoSortedLists (合并两个有序链表)
问题描述：[LeedCode](https://leetcode-cn.com/problems/merge-two-sorted-lists/)   
解决代码：
``` java
/**
 * 数据结构：链表
 * leetcode：https://leetcode-cn.com/problems/merge-two-sorted-lists/
 * 合并两个有序链表
 * */
public class MergeTwoSortedLists {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null){
            return l2;
        }
        if(l2 == null){
            return l1;
        }
        if(l1.val <= l2.val){
            l1.next= mergeTwoLists(l1.next,l2);
            return l1;
        }else{
            ListNode next2 = l1.next;
            l2.next = mergeTwoLists(l1,l2.next);
            return l2;
        }

    }
}
```
## 3. IntersectionOfTwoLinkedLists (找出两个链表的交点)
问题描述：[LeedCode](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)   
解决代码：
``` java
```
## 4. IntersectionOfTwoLinkedLists (找出两个链表的交点)
问题描述：[LeedCode](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)   
解决代码：
``` java
```

