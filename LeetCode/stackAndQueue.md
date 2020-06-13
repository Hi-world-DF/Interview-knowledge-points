# 栈和队列
* [1. ImplementQueueUsingStacks（用栈实现队列）]()
* [2. ImplementStackUsingQueues（用队列实现栈）]()
* [3. MinStack（最小栈）]()
* [4. ValidParentheses（有效括号,括号匹配问题）]()
* [5. DailyTemperatures（每日温度）]()
* []()

## 1. ImplementQueueUsingStacks（用栈实现队列）
问题描述：[LeedCode](https://leetcode-cn.com/problems/implement-queue-using-stacks/)   
解决代码：
``` java
import java.util.Stack;

/**
 * 数据结构：栈和队列
 * leetcode：https://leetcode-cn.com/problems/implement-queue-using-stacks/
 * 用栈实现队列
 * */
public class ImplementQueueUsingStacks {
    private Stack<Integer> in = new Stack<>();
    private Stack<Integer> out = new Stack<>();
    /** Initialize your data structure here. */
    public ImplementQueueUsingStacks() {

    }

    /** Push element x to the back of queue. */
    public void push(int x) {
        in.push(x);
    }

    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if(out.isEmpty()){
            while(!in.isEmpty()){
                 out.push(in.pop());
            }
        }
        return out.pop();
    }

    /** Get the front element. */
    public int peek() {
        if(out.isEmpty()){
            while(!in.isEmpty()){
                out.push(in.pop());
            }
        }
        return out.peek();
    }

    /** Returns whether the queue is empty. */
    public boolean empty() {
        if(in.isEmpty() && out.isEmpty()){
            return true;
        }else{
            return false;
        }
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```
## 2. ImplementStackUsingQueues（用队列实现栈）
问题描述：[LeedCode](https://leetcode-cn.com/problems/implement-stack-using-queues/)   
解决代码：
``` java
/**
 * 数据结构：栈和队列
 * leetcode：https://leetcode-cn.com/problems/implement-stack-using-queues/
 * 用队列实现栈
 * */
import java.util.LinkedList;
import java.util.Queue;

public class ImplementStackUsingQueues {
    private Queue<Integer> queue;
    /** Initialize your data structure here. */
    public ImplementStackUsingQueues() {
        queue = new LinkedList<>();
    }

    /** Push element x onto stack. */
    public void push(int x) {
        queue.add(x);
        int size = queue.size();
        while(size > 1){
            queue.add(queue.poll());
            size--;
        }
    }

    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        return queue.poll();
    }

    /** Get the top element. */
    public int top() {
        return queue.peek();
    }

    /** Returns whether the stack is empty. */
    public boolean empty() {
        return queue.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```
## 3. MinStack（最小栈）
问题描述：[LeedCode](https://leetcode-cn.com/problems/min-stack/)   
解决代码：
``` java
/**
 * 数据结构：栈和队列
 * leetcode：https://leetcode-cn.com/problems/min-stack/
 * 最小栈
 * */
import java.util.Stack;

public class MinStack {
    private Stack<Integer> dataStack;
    private Stack<Integer> minStack;
    private int min;
    /** initialize your data structure here. */
    //两个栈，一个正常存数据，另一个存当前栈内最小的那个值，
    public MinStack() {
        dataStack = new Stack<>();
        minStack = new Stack<>();
        min = Integer.MAX_VALUE;
    }
    // dataStack每push一个数,同时minStack也push一个当前最小的值
    public void push(int x) {
        dataStack.add(x);
        min = Math.min(min,x);
        minStack.add(min);
    }
    // pop时两个栈同时pop(),只要min栈不空，那么min就是min栈顶的那个值
    public void pop() {
        dataStack.pop();
        minStack.pop();
        if(minStack.isEmpty()){
            min = Integer.MAX_VALUE;
        }else{
            min = minStack.peek();
        }
    }

    public int top() {
        return dataStack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```
## 4. ValidParentheses（有效括号,括号匹配问题）
问题描述：[LeedCode](https://leetcode-cn.com/problems/valid-parentheses/)   
解决代码：
``` java
import java.util.Stack;

/**
 * 数据结构：栈和队列
 * leetcode：https://leetcode-cn.com/problems/valid-parentheses/
 * 有效括号
 * */
public class ValidParentheses {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for(int i = 0;i < s.length();i++){
            char currentP = s.charAt(i);
            if(currentP == '(' || currentP == '[' || currentP == '{'){
                stack.push(currentP);
            }else{
                if(currentP == ')'){
                     if(stack.peek()=='('){
                         stack.pop();
                         continue;
                     }else{
                         return false;
                     }
                }
                if(currentP == ']'){
                    if(stack.peek()=='['){
                        stack.pop();
                        continue;
                    }else{
                        return false;
                    }
                }
                if(currentP == '}'){
                    if(stack.peek()=='{'){
                        stack.pop();
                        continue;
                    }else{
                        return false;
                    }
                }
            }
        }
        return stack.isEmpty();
    }
}
```
## 5. DailyTemperatures（每日温度）
问题描述：[LeedCode](https://leetcode-cn.com/problems/daily-temperatures/)   
解决代码：
``` java
import java.util.Stack;

/**
 * 数据结构：栈和队列
 * leetcode：https://leetcode-cn.com/problems/daily-temperatures/
 * 每日温度
 * */
public class DailyTemperatures {
    //方法一：暴力破解
    public int[] dailyTemperatures1(int[] T) {
        int n = T.length;
        int[] result = new int[n];

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (T[j] > T[i]) {
                    result[i] = j - i;
                    break;
                }
            }

        }
        return result;
    }

    //方法二：单调栈
    public int[] dailyTemperatures2(int[] T) {
        int n = T.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();
        for(int i = 0;i < n;i++){
            while(!stack.isEmpty() && T[i] > T[stack.peek()]){
                int value = stack.pop();
                result[value] = i - value;
            }
            stack.add(i);
        }
        return result;
    }
}
```




