# 链表
* [1. IntersectionOfTwoLinkedLists (找出两个链表的交点)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#1-intersectionoftwolinkedlists-%E6%89%BE%E5%87%BA%E4%B8%A4%E4%B8%AA%E9%93%BE%E8%A1%A8%E7%9A%84%E4%BA%A4%E7%82%B9)
* [2. MergeTwoSortedLists (合并两个有序链表)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#2-mergetwosortedlists-%E5%90%88%E5%B9%B6%E4%B8%A4%E4%B8%AA%E6%9C%89%E5%BA%8F%E9%93%BE%E8%A1%A8)
* [3. RemoveDuplicatesFromSortedList (删除有序链表中重复元素)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#3-removeduplicatesfromsortedlist-%E5%88%A0%E9%99%A4%E6%9C%89%E5%BA%8F%E9%93%BE%E8%A1%A8%E4%B8%AD%E9%87%8D%E5%A4%8D%E5%85%83%E7%B4%A0)
* [4. ReverseLinkedList (链表反转)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#4-reverselinkedlist-%E9%93%BE%E8%A1%A8%E5%8F%8D%E8%BD%AC)
* [5. RemoveNthNodeFromEndOfList (删除链表倒数第n个节点)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#5-removenthnodefromendoflist-%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E5%80%92%E6%95%B0%E7%AC%ACn%E4%B8%AA%E8%8A%82%E7%82%B9)
* [6. SwapNodesInPairs (两两交换链表中的节点)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#6-swapnodesinpairs-%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9)
* [7. AddTwoNumbersFromList (两个链表求和)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#7-addtwonumbersfromlist-%E4%B8%A4%E4%B8%AA%E9%93%BE%E8%A1%A8%E6%B1%82%E5%92%8C)
* [8. PalindromeLinkedList (回文链表)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#8-palindromelinkedlist-%E5%9B%9E%E6%96%87%E9%93%BE%E8%A1%A8)
* [9. SplitLinkedListInParts (分隔链表)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/linkList.md#9-splitlinkedlistinparts-%E5%88%86%E9%9A%94%E9%93%BE%E8%A1%A8)
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
## 5. RemoveNthNodeFromEndOfList (删除链表倒数第n个节点)
问题描述：[LeedCode](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)   
解决代码：
``` java
/**
 * 数据结构：链表
 * leetcode：https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/
 * 删除链表倒数第n个节点
 * */
public class RemoveNthNodeFromEndOfList {
    /**
     * 方法一：
     * */
    public ListNode removeNthFromEnd(ListNode head, int n) {
        //求整个list有多少个节点，然后找到倒数第n个元素
        ListNode length = head;
        int l = 0;
        while(length !=null){
            l++;
            length = length.next;
        }
        //倒数第n个元素位置
        int nums = l-n;
        ListNode listNode = head;
        //如果要删除最前面的元素，那就返回head.next
        if(nums == 0){
            return head.next;
        }
        //然后找到倒数第n个位置元素
        while(nums > 1){
            nums--;
            listNode= listNode.next;
        }
        //如果head是null那就返回null,否则就将要删除的元素的前一个元素指向它的后一个元素
        if(head == null){
            return null;
        }else{
            listNode.next = listNode.next.next;
        }
        return head;
    }

    /**
     * 方法二：
     * */
    public ListNode removeNthFromEnd2(ListNode head, int n) {
        //指向第n个节点
        ListNode last = head;
        while(n > 0){
            last = last.next;
            n--;
        }
        //指向前面的节点
        ListNode first = head;
        //删除第一个元素
        if(last == null){
            return head.next;
        }
        while(last.next != null){
            last = last.next;
            first = first.next;
        }
        first.next = first.next.next;
        return head;
    }
}
```
## 6. SwapNodesInPairs (两两交换链表中的节点)
问题描述：[LeedCode](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)   
解决代码：
``` java
/**
 * 数据结构：链表
 * leetcode：https://leetcode-cn.com/problems/swap-nodes-in-pairs/
 * 两两交换链表中的节点
 * */
public class SwapNodesInPairs {
    public ListNode swapPairs(ListNode head) {
        //首先判断是否为空或者只有一个节点，是就返回该null/节点
        if(head == null || head.next == null){
            return head;
        }
        //两个指针分别指向前后两个节点
        ListNode pre = head;
        ListNode last = pre.next;
        while(last != null){
            //交换两节点的值
            int tmp = last.val;
            last.val = pre.val;
            pre.val = tmp;
            //如果后一指针没有节点，那么跳出循环
            if(last.next == null){
                break;
            }
            //两个指针都向后面移动两个位置
            pre = pre.next.next;
            last = last.next.next;
        }
        return head;
    }
}
```
## 7. AddTwoNumbersFromList (两个链表求和)
问题描述：[LeedCode](https://leetcode-cn.com/problems/add-two-numbers-ii/)   
解决代码：
``` java
/**
 * 数据结构：链表
 * leetcode：https://leetcode-cn.com/problems/add-two-numbers-ii/
 * 链表求和
 * */
public class AddTwoNumbersFromList {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if(l1 == null){
            return l2;
        }
        if(l2 == null){
            return l1;
        }
        //使用栈让链表的元素从最后一个节点相加
        Stack<Integer> s1 = new Stack<>();
        Stack<Integer> s2 = new Stack<>();
        ListNode newHead = new ListNode(-1);
        //将l1的节点放到栈1中
        while(l1 != null){
            s1.push(l1.val);
            l1 = l1.next;
        }
        //将l2的节点放到栈2中
        while(l2 != null){
            s2.push(l2.val);
            l2 = l2.next;
        }
        //定义进位
        int carry = 0;
        //当所有节点都添加完，循环结束
        while(!s1.isEmpty() || !s2.isEmpty() || carry != 0){
            int a = s1.isEmpty()? 0 : s1.pop();
            int b = s2.isEmpty()? 0 : s2.pop();
            int sum = a + b + carry;
            ListNode node = new ListNode(sum % 10);
            //头插法把节点放在第一个位置
            node.next = newHead.next;
            newHead.next = node;
            carry = sum/10;
        }
        return newHead.next;
    }
}
```

## 8. PalindromeLinkedList (回文链表)
问题描述：[LeedCode](https://leetcode-cn.com/problems/palindrome-linked-list/)   
解决代码：
方法一：没通过
``` java
/**
 * 数据结构：链表
 * leetcode：https://leetcode-cn.com/problems/palindrome-linked-list/
 * 回文链表
 * >>>>>>>>>>>>>>>>>>>>>>>未通过
 * */
public class PalindromeLinkedList {
     public boolean isPalindrome(ListNode head) {
        Stack<Integer> s = new Stack<>();
        //如果链表为空，或者只有一个元素，那么返回true
        if(head == null || head.next == null){
            return true;
        }
        //n来计数，链表有多少个节点
        int n = 0;
        ListNode node = head;
        while(node != null){
            n++;
            node = node.next;
        }
        int sn = (n+1)/2;
        int mid = n/2 +1;
        ListNode sNode = head;
        while(sn > 0){
            s.push(sNode.val);
            sNode = sNode.next;
            sn--;
        }
        while(mid > 0){
            head = head.next;
            mid--;
        }
        while(!s.isEmpty()){
            if(s.pop() != head.val){
                return false;
            }
            head = head.next;
        }
        return true;
    }
}
```
方法二：
``` java
/**
 * 数据结构：链表
 * leetcode：https://leetcode-cn.com/problems/palindrome-linked-list/
 * 回文链表
 * */
public class PalindromeLinkedList {

    public boolean isPalindrome(ListNode head){
        if(head == null || head.next == null){
            return true;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        if(fast != null){
            slow = slow.next;
        }
        cut(head,slow);
        return isEqual(head,reverse(slow));
    }

    private boolean isEqual(ListNode l1, ListNode l2) {
        while(l1 != null && l2 != null){
            if(l1.val != l2.val){
                return false;
            }
            l1 = l1.next;
            l2 = l2.next;
        }
        return true;
    }

    private ListNode reverse(ListNode slow) {
        ListNode newHead = null;
        while(slow != null){
            ListNode nextNode = slow.next;
            slow.next = newHead;
            newHead = slow;
            slow = nextNode;
        }
        return newHead;
    }

    private void cut(ListNode head, ListNode slow) {
        while(head.next != slow){
            head = head.next;
        }
        head.next = null;
    }
}
```
## 9. SplitLinkedListInParts (分隔链表)
问题描述：[LeedCode](https://leetcode-cn.com/problems/split-linked-list-in-parts/)   
解决代码：
``` java
/**
 * 数据结构：链表
 * leetcode：https://leetcode-cn.com/problems/split-linked-list-in-parts/
 * 分隔链表
 * */
public class SplitLinkedListInParts {
    public ListNode[] splitListToParts(ListNode root, int k) {
        int n = 0;
        ListNode current = root;
        //确定链表共有多少个节点
        while(current != null){
            n++;
            current = current.next;
        }
        /**
         * 分割之后链表的节点个数，前mod个链表的节点个数为size+1，之后的为size
         * 若N<k,则前面每个链表为一个元素，后面的为空
         */
        int mod = n%k;
        int size = n/k;
        ListNode[] result = new ListNode[k];
        current = root;
        //给ListNode[]数组的每个链表元素循环赋值
        for(int i = 0; current != null && i < k;i++){
            result[i] = current;
            int currentSize = size;
            if(mod > 0){
                currentSize = currentSize + 1;
                mod--;
            }
            for(int j = 0; j < currentSize-1; j++){
                current = current.next;
            }
            //ListNode[]数组里的每个链表元素结尾要指向null;
            ListNode next = current.next;
            current.next = null;
            current = next;
        }
        return result;
    }
}
```


