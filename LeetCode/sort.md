# 经典的各种排序算法
* [选择排序]()
* [插入排序]()

## 1.选择排序


代码：
``` 
package sortAll;

/**
 * 2020/05/23
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
