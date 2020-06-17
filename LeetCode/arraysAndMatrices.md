# 数组和矩阵
* [1.MaxConsecutiveOnes（最大连续1的个数）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#1maxconsecutiveones%E6%9C%80%E5%A4%A7%E8%BF%9E%E7%BB%AD1%E7%9A%84%E4%B8%AA%E6%95%B0)
* [2.MoveZeroes（移动零到数组末尾）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#2movezeroes%E7%A7%BB%E5%8A%A8%E9%9B%B6%E5%88%B0%E6%95%B0%E7%BB%84%E6%9C%AB%E5%B0%BE)
* [3.ReshapeTheMatrix（重塑矩阵）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#3reshapethematrix%E9%87%8D%E5%A1%91%E7%9F%A9%E9%98%B5)
* [4.SearchA2dMatrixII（搜索二维矩阵）]()
* [5.KthSmallestElementInASortedMatrix（有序矩阵中第k小的元素）]()
## 1.MaxConsecutiveOnes（最大连续1的个数）
问题描述：[LeetCode](https://leetcode-cn.com/problems/max-consecutive-ones/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/max-consecutive-ones/
 * 题目描述：最大连续1的个数
 * */
public class MaxConsecutiveOnes {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max = 0;
        int current = 0;
        for(int num : nums){
            current = num == 0?0:current+1;
            max = Math.max(max,current);
            //max = max>current?max:current;
        }
        return max;
    }
    public static void main(String[] args){

    }
}
```
## 2.MoveZeroes（移动零到数组末尾）
问题描述：[LeetCode](https://leetcode-cn.com/problems/move-zeroes/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/move-zeroes/
 * 题目描述：移动零到数组末尾
 * */
public class MoveZeroes {
    public void moveZeroes(int[] nums) {
        int n = nums.length;
        int notZero = 0;
        for(int i = 0; i < n;i++){
            if(nums[i] != 0){
                nums[notZero] = nums[i];
                notZero++;
            }
        }
        while(notZero < n){
            nums[notZero] = 0;
            notZero++;
        }
    }
}
```
## 3.ReshapeTheMatrix（重塑矩阵）
问题描述：[LeetCode](https://leetcode-cn.com/problems/reshape-the-matrix/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/reshape-the-matrix/
 * 题目描述：重塑矩阵
 * */
public class ReshapeTheMatrix {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int[][] result = new int[r][c];
        int m = nums.length;
        int n = nums[0].length;
        int[] num = new int[m*n];
        for(int i = 0,x=0;i < m;i++){
            for(int j = 0;j < n;j++){
                num[x] = nums[i][j];
                x++;
            }
        }
        for(int i = 0; i < num.length;i++){
            System.out.print(num[i]+" ");
        }
        System.out.println();
        if(m*n < r*c){
            return nums;
        }
        for(int i = 0,y=0;i < r;i++){
            for(int j = 0;j < c;j++){
                result[i][j] = num[y];
                y++;
            }
        }
        return result;
    }
}
```
## 4.SearchA2dMatrixII（搜索二维矩阵）
问题描述：[LeetCode](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/search-a-2d-matrix-ii/
 * 题目描述：搜索二维矩阵
 * */
public class SearchA2dMatrixII {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0 || matrix[0].length == 0){
            return false;
        }
        int m = matrix.length;
        int n = matrix[0].length;
        int row = 0;
        int column = n-1;
        while(row < m && column >= 0){
            if(matrix[row][column] == target){
                return true;
            }else if(matrix[row][column] > target){
                column--;
            }else{
                row++;
            }
        }
        return false;
    }
}
```
## 5.KthSmallestElementInASortedMatrix（有序矩阵中第k小的元素）
问题描述：[LeetCode](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/)   
代码：
``` java 
import java.util.Arrays;
import java.util.PriorityQueue;

/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/
 * 题目描述：有序矩阵中第k小的元素
 * */
public class KthSmallestElementInASortedMatrix {
    /**
     * 方法一：降维处理，数组排序，输出第k-1个元素
     * */
    public int kthSmallest(int[][] matrix, int k) {
        if(matrix == null || matrix.length == 0||matrix[0].length == 0){
            return -1;
        }
        int m = matrix.length;
        int n = matrix[0].length;
        int[] nums = new int[m*n];
        int l = 0;
        for(int i = 0;i < m;i++){
            for(int j = 0;j < n;j++){
                nums[l] = matrix[i][j];
                l++;
            }
        }
        Arrays.sort(nums);
        return nums[k-1];
    }
    /**
     * 方法二：二分查找
     * */
    public int kthSmallest1(int[][] matrix, int k) {
        int m = matrix.length;
        int n = matrix[0].length;
        int low = matrix[0][0];
        int high = matrix[m-1][n-1];
        while(low <= high){
            int mid = low + (high - low)/2;
            int cnt = 0;
            for(int i = 0;i < m;i++){
                for(int j = 0;j < n;j++){
                    if(matrix[i][j] <= mid){
                        cnt++;
                    }
                }
            }
            if(cnt < k){
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }
        return low;
    }
    /**
     * 方法三：利用堆求解（有点难）
     * */
    public int kthSmallest2(int[][] matrix, int k) {
        int m = matrix.length;
        int n = matrix[0].length;
        PriorityQueue<Tuple> pq = new PriorityQueue<>();
        for(int i = 0;i < n;i++){
            pq.offer(new Tuple(0,i,matrix[0][i]));
        }
        for(int j = 0;j < k-1;j++){
            Tuple t = pq.poll();
            if(t.x == m-1){
                continue;
            }
            pq.offer(new Tuple(t.x+1,t.y,matrix[t.x+1][t.y]));
        }
        return pq.poll().val;
    }
}

class Tuple implements Comparable<Tuple> {
    int x, y, val;
    public Tuple(int x, int y, int val) {
        this.x = x; this.y = y; this.val = val;
    }
    @Override
    public int compareTo(Tuple that) {
        return this.val - that.val;
    }
}
```
