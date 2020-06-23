# 数组和矩阵
* [1.MaxConsecutiveOnes（最大连续1的个数）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#1maxconsecutiveones%E6%9C%80%E5%A4%A7%E8%BF%9E%E7%BB%AD1%E7%9A%84%E4%B8%AA%E6%95%B0)
* [2.MoveZeroes（移动零到数组末尾）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#2movezeroes%E7%A7%BB%E5%8A%A8%E9%9B%B6%E5%88%B0%E6%95%B0%E7%BB%84%E6%9C%AB%E5%B0%BE)
* [3.ReshapeTheMatrix（重塑矩阵）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#3reshapethematrix%E9%87%8D%E5%A1%91%E7%9F%A9%E9%98%B5)
* [4.SearchA2dMatrixII（搜索二维矩阵）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#4searcha2dmatrixii%E6%90%9C%E7%B4%A2%E4%BA%8C%E7%BB%B4%E7%9F%A9%E9%98%B5)
* [5.KthSmallestElementInASortedMatrix（有序矩阵中第k小的元素）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#5kthsmallestelementinasortedmatrix%E6%9C%89%E5%BA%8F%E7%9F%A9%E9%98%B5%E4%B8%AD%E7%AC%ACk%E5%B0%8F%E7%9A%84%E5%85%83%E7%B4%A0)
* [6.FindTheDuplicateNumber（寻找重复的数）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#6findtheduplicatenumber%E5%AF%BB%E6%89%BE%E9%87%8D%E5%A4%8D%E7%9A%84%E6%95%B0)
* [7.SetMismatch（错误的集合）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#7setmismatch%E9%94%99%E8%AF%AF%E7%9A%84%E9%9B%86%E5%90%88)
* [8.DegreeOfAnArray（数组的度）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#8degreeofanarray%E6%95%B0%E7%BB%84%E7%9A%84%E5%BA%A6)
* [9.BeautifulArrangementII（优美的排列）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#9beautifularrangementii%E4%BC%98%E7%BE%8E%E7%9A%84%E6%8E%92%E5%88%97)
* [10.ToeplitzMatrix（托普利茨矩阵-对角元素相等的矩阵）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#10toeplitzmatrix%E6%89%98%E6%99%AE%E5%88%A9%E8%8C%A8%E7%9F%A9%E9%98%B5-%E5%AF%B9%E8%A7%92%E5%85%83%E7%B4%A0%E7%9B%B8%E7%AD%89%E7%9A%84%E7%9F%A9%E9%98%B5)
* [11.MaxChunksToMakeSorted（最多能完成排序的块）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#11maxchunkstomakesorted%E6%9C%80%E5%A4%9A%E8%83%BD%E5%AE%8C%E6%88%90%E6%8E%92%E5%BA%8F%E7%9A%84%E5%9D%97)
* [12.ArrayNesting（数组嵌套）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/arraysAndMatrices.md#12arraynesting%E6%95%B0%E7%BB%84%E5%B5%8C%E5%A5%97)
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
## 6.FindTheDuplicateNumber（寻找重复的数）
问题描述：[LeetCode](https://leetcode-cn.com/problems/find-the-duplicate-number/)   
代码：
``` java 
import java.util.Arrays;

/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/find-the-duplicate-number/
 * 题目描述：寻找重复的数
 * */
public class FindTheDuplicateNumber {
    //方法一：排序
    public int findDuplicate(int[] nums) {
        if(nums == null || nums.length==0){
            return -1;
        }
        int n = nums.length;
        Arrays.sort(nums);
        for(int i = 0;i < n;i++){
            if(i+1 < n && nums[i+1]==nums[i]){
                return nums[i];
            }
        }
        return -1;
    }
    //方法二：二分查找
    public int findDuplicate1(int[] nums) {
        int low = 1;
        int high = nums.length -1;
        while(low < high){
            int mid = low +(high - low)/2;
            int n = 0;
            for(int i = 0;i<nums.length;i++){
                if(nums[i] <= mid){
                    n++;
                }
            }
            if(mid < n){
                high = mid-1;
            }else{
                low = mid+1;
            }
        }
        return low;
    }
    //方法三：双指针
    public int findDuplicate2(int[] nums) {
        return 0;
    }
}
```
## 7.SetMismatch（错误的集合）
问题描述：[LeetCode](https://leetcode-cn.com/problems/set-mismatch/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/set-mismatch/
 * 题目描述：错误的集合
 * */
public class SetMismatch {
    /**
     * 方法一：对数组排序
     * */
    public int[] findErrorNums(int[] nums) {
        int n = nums.length;
        //结果数组只有两个元素：一个是数组中重复的那个元素，一个是缺少的那个元素
        int[] result = new int[2];
        //对数组排序
        Arrays.sort(nums);
        for(int i = 0;i < n;i++){
            if(i+1 < n && nums[i] == nums[i+1]){
                //排序后前后相同的元素就是重复的元素
                result[0] = nums[i];
            }
            if(i+1< n && nums[i+1] - nums[i] == 2){
                //排序后当前后两个元素相差为2，那么中间的元素即为缺失元素
                result[1] = nums[i]+1;
            }
        }
        //但要考虑缺失第一个元素1或者最后一个元素n
        if(result[1] == 0){
            if(nums[0] != 1){
                result[1] = 1;
            }else{
                result[1] = n-1;
            }
        }
        return result;
    }
    /**
     * 方法二：对数组元素进行交换，使元素在对应的位置
     * */
    public int[] findErrorNums1(int[] nums) {
        int n = nums.length;
        for(int i = 0;i < n;i++){
            while(nums[i] != i+1 && nums[nums[i]-1] != nums[i]){
                int temp = nums[i];
                nums[i] = nums[nums[i] -1];
                nums[nums[i]-1] = temp;
            }
        }
        for(int i = 0;i < n;i++){
            if(nums[i] != i+1){
                return new int[]{nums[i],i+1};
            }
        }
        return null;
    }

    public static void main(String[] args){
        int[] a = {3,2,3,4,6,5};
        SetMismatch setMismatch = new SetMismatch();
        int[] result = setMismatch.findErrorNums(a);
        System.out.println(result[0]+" "+result[1]);
    }

}
```

## 8.DegreeOfAnArray（数组的度）
问题描述：[LeetCode](https://leetcode-cn.com/problems/degree-of-an-array/)   
代码：
``` java 
import java.util.HashMap;
import java.util.Map;

/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/degree-of-an-array/
 * 题目描述：数组的度
 * */
public class DegreeOfAnArray {
    public int findShortestSubArray(int[] nums) {
        /**current用来找nums的度及对应的数字;
         * lastIndex用来记录数字最后出现的位置;
         * firstIndex用来记录数字最后出现的位置
         */
        Map<Integer,Integer> current = new HashMap<>();
        Map<Integer,Integer> lastIndex = new HashMap<>();
        Map<Integer,Integer> firstIndex = new HashMap<>();
        for(int i = 0;i < nums.length;i++){
            //如果map中没有nums[i]的key，则nums[i]的value设为0+1;否则就是它的value+1;
            current.put(nums[i],current.getOrDefault(nums[i],0)+1);
            lastIndex.put(nums[i],i);
            if(!firstIndex.containsKey(nums[i])){
                firstIndex.put(nums[i],i);
            }
        }
        /**
         * 现在：
         * current放了所有num的key和value;key是数字，value是;
         * lastIndex用来记录数字最后出现的位置;
         * firstIndex用来记录数字第一次出现的位置
         */
        int maxDu = 0;
        for(int num : nums){
            maxDu = maxDu >= current.get(num)?maxDu:current.get(num);
        }
        int resultL = nums.length;
        for(int i = 0;i < nums.length; i++){
            int num = nums[i];
            int currentNum = current.get(num);
            if(currentNum != maxDu){
                continue;
            }
            resultL = Math.min(resultL,lastIndex.get(num) - firstIndex.get(num)+1);
        }
        return resultL;
    }
    public static void main(String[] args){
        DegreeOfAnArray degreeOfAnArray = new DegreeOfAnArray();
        int[] a = {2,1,2,2,4,4,5,1};
        int result = degreeOfAnArray.findShortestSubArray(a);
        System.out.println(result);
    }
}
```
## 9.BeautifulArrangementII（优美的排列）
问题描述：[LeetCode](https://leetcode-cn.com/problems/beautiful-arrangement-ii/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/beautiful-arrangement-ii/
 * 题目描述：优美的排列
 * */
public class BeautifulArrangementII {
    public int[] constructArray(int n, int k) {
        int[] result = new int[n];
        result[0] = 1;
        int interval = k;
        for(int i = 1;i <= k; i++){
            result[i] = i%2 == 1?result[i-1]+interval:result[i-1]-interval;
            interval--;
        }
        for(int i = k+1;i < n;i++){
            result[i] = i+1;
        }
        return result;
    }
}
```
## 10.ToeplitzMatrix（托普利茨矩阵-对角元素相等的矩阵）
问题描述：[LeetCode](https://leetcode-cn.com/problems/toeplitz-matrix/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/toeplitz-matrix/
 * 题目描述：托普利茨矩阵(对角元素相等的矩阵)
 * */
public class ToeplitzMatrix {
    public boolean isToeplitzMatrix(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        for(int i = 0;i < m;i++){
            if(!check(matrix,matrix[i][0],i,0)){
                return false;
            }
        }
        for(int j = 0;j < n;j++){
            if(!check(matrix,matrix[0][j],0,j)){
                return false;
            }
        }
        return true;
    }

    private boolean check(int[][] matrix, int value, int row, int col) {
        int m = matrix.length;
        int n = matrix[0].length;
        if(row >= m || col >= n){
            return true;
        }
        if(matrix[row][col] != value){
            return false;
        }
        return check(matrix, value, row+1, col+1);
    }
}
```
## 11.MaxChunksToMakeSorted（最多能完成排序的块）
问题描述：[LeetCode](https://leetcode-cn.com/problems/max-chunks-to-make-sorted/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/max-chunks-to-make-sorted/
 * 题目描述： 最多能完成排序的块
 * */
public class MaxChunksToMakeSorted {
    public int maxChunksToSorted(int[] arr) {
        if(arr == null){
            return 0;
        }
        int num = 0;
        int current = arr[0];
        for(int i = 0;i < arr.length;i++){
            current = Math.max(current,arr[i]);
            if(current == i){
                num++;
            }
        }
        return num;
    }
}
```
## 12.ArrayNesting（数组嵌套）
问题描述：[LeetCode](https://leetcode-cn.com/problems/array-nesting/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/array-nesting/
 * 题目描述：数组嵌套
 * */
public class ArrayNesting {
    public int arrayNesting(int[] nums) {
        int max = 0;
        for(int i =0;i < nums.length;i++){
            //用来计算可以嵌套的层数
            int current = 0;
            for(int j = i;nums[j] != -1;){
                current++;
                int tmp = nums[j];
                //用来标记嵌套（访问）过的位置
                nums[j] = -1;
                j = tmp;
            }
            //每个位置开始都有一个嵌套层数，取最大的输出
            max = Math.max(max,current);
        }
        return max;
    }
}
```
