# 经典的各种排序算法
* [选择排序](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/sort.md#1%E9%80%89%E6%8B%A9%E6%8E%92%E5%BA%8F)
* [插入排序](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/sort.md#2%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F)
* [希尔排序](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/sort.md#3%E5%B8%8C%E5%B0%94%E6%8E%92%E5%BA%8F)

## 1.选择排序
算法思想：
代码：
``` java 
package sortAll;

/**
 * 选择排序
 * */
public class Selection {
    public static void sort(int[] a){
        //将a[]按升序排列
        int n = a.length;
        for(int i = 0;i < n;i++) {
            int min = i;
            //将a[i]和最小元素交换
            for (int j = 0; j < n; j++) {
                if (less(a[min], a[j])) {
                    min = j;
                }
                exch(a, i, min);
            }
        }
    }

    private static void exch(int[] a, int i, int min) {
        int temp = a[min];
        a[min] = a[i];
        a[i] = temp;
    }

    private static boolean less(int a, int b) {
        if(a < b){
            return true;
        }else{
            return false;
        }
    }

    private static void show(int[] a){
        for(int i=0;i<a.length;i++){
            System.out.print(a[i]+" ");
        }
    }

    public static void main(String[] args){
        int[] a = {12,23,1,12,23,13,44};
        sort(a);
        show(a);
    }

}
```

## 2.插入排序
算法思想：
代码：
``` java
package sortAll;

public class Insertion {
    public static void sort(int[] a){
        int n = a.length;
        for(int i = 1;i < n;i++){
            for(int j = 0;j<i;j++){
                if(less(a[i],a[j])){
                    swap(a,i,j);
                }
            }
        }
    }

    private static void swap(int[] a, int j, int i) {
        int temp = a[j];
        a[j] = a[i];
        a[i] = temp;
    }

    private static boolean less(int a, int b) {
        if(a > b){
            return false;
        }else {
            return true;
        }
    }

    private static void show(int[] a){
        for(int i=0;i<a.length;i++){
            System.out.print(a[i]+" ");
        }
    }

    public static void main(String[] args){
        int[] a = {1,23,12,8,9,21,4,0,16,3,5,18};
        sort(a);
        show(a);
    }
}
```

## 3.希尔排序
算法思想：
代码：
``` java
package sortAll;
/**
 * 希尔排序
 * */
public class Shell {
    public static void sort(int[] a){
        int n = a.length;
        int h =1;
        while (h < n/3){
            h = 3*h +1;
        }
        while (h >= 1){
            for(int i = h;i < n;i++){
                for(int j = i;j >= h && less(a[j],a[j-h]);j-=h){
                    exchange(a,j,j-h);
                }
            }
            h = h/3;
        }
    }
    /**
     * 交换
     * */
    private static void exchange(int[] a, int j, int i) {
        if(a[j] < a[i]){
            int temp = a[j];
            a[j] = a[i];
            a[i] = temp;
        }
    }
    /**
     * 比较
     * */
    private static boolean less(int a, int b) {
        if(a < b){
            return true;
        }
        return false;
    }
    private static void isSorted(int[] a){
        for(int i = 0;i < a.length;i++){
            System.out.print(a[i]+" ");
        }
    }
    /**
     * 测试
     * */
    public static void main(String[] args){
        int[] a = {2,3,1,7,12,32,6,2,5};
        Shell.sort(a);
        Shell.isSorted(a);
    }
}

```
