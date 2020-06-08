# 链表
* [1. IntersectionOfTwoLinkedLists (找出两个链表的交点)]()

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
