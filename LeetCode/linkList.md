# 链表
* [1. IntersectionOfTwoLinkedLists (找出两个链表的交点)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#1-intersectionoftwolinkedlists-%E6%89%BE%E5%87%BA%E4%B8%A4%E4%B8%AA%E9%93%BE%E8%A1%A8%E7%9A%84%E4%BA%A4%E7%82%B9)
* [2. MergeTwoSortedLists (合并两个有序链表)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#2-mergetwosortedlists-%E5%90%88%E5%B9%B6%E4%B8%A4%E4%B8%AA%E6%9C%89%E5%BA%8F%E9%93%BE%E8%A1%A8)
* [3. RemoveDuplicatesFromSortedList (删除有序链表中重复元素)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#3-removeduplicatesfromsortedlist-%E5%88%A0%E9%99%A4%E6%9C%89%E5%BA%8F%E9%93%BE%E8%A1%A8%E4%B8%AD%E9%87%8D%E5%A4%8D%E5%85%83%E7%B4%A0)
* [4. ReverseLinkedList (链表反转)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#4-reverselinkedlist-%E9%93%BE%E8%A1%A8%E5%8F%8D%E8%BD%AC)
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
## 3. RemoveDuplicatesFromSortedList (删除有序链表中重复元素)
问题描述：[LeedCode](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)   
解决代码：
``` java
/**
 * 数据结构：链表
 * leetcode：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/
 * 删除有序链表中重复元素
 * */
public class RemoveDuplicatesFromSortedList {
    public ListNode deleteDuplicates(ListNode head){
        if(head == null || head.next == null){
            return head;
        }
        head.next = deleteDuplicates(head.next);
        if(head.val == head.next.val){
            return head.next;
        }else{
            return head;
        }
    }
}
```
## 4. ReverseLinkedList (链表反转)
问题描述：[LeedCode](https://leetcode-cn.com/problems/reverse-linked-list/)   
解决代码：
``` java
/**
 * 数据结构：链表
 * leetcode：https://leetcode-cn.com/problems/reverse-linked-list/
 * 链表反转
 * */
public class ReverseLinkedList {
    /**
     * 递归
     * */
//    public ListNode reverseList(ListNode head){
//        if(head == null || head.next == null){
//            return head;
//        }
//        ListNode next = head.next;
//        ListNode newHead = reverseList(next);
//        next.next = head;
//        head.next = null;
//        return newHead;
//    }
        /**
         * 头插法
         * */
        public ListNode reverseList(ListNode head){
            ListNode newHead = new ListNode(-1);
            while(head != null){
                ListNode next = head.next;
                head.next = newHead.next;
                newHead.next = head;
                head = next;
            }
            return newHead;
        }
}
```

