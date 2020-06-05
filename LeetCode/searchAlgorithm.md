# 搜索算法
* [BFS(广度优先算法)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/searchAlgorithm.md#%E4%B8%80bfs)
  * [1. ShortestPathBinaryMatrix（二进制矩阵中的最短路径）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/searchAlgorithm.md#1-shortestpathbinarymatrix%E4%BA%8C%E8%BF%9B%E5%88%B6%E7%9F%A9%E9%98%B5%E4%B8%AD%E7%9A%84%E6%9C%80%E7%9F%AD%E8%B7%AF%E5%BE%84)
* [DFS(深度优先算法)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/searchAlgorithm.md#%E4%BA%8Cdfs)

# 一、BFS
## 1. ShortestPathBinaryMatrix（二进制矩阵中的最短路径）
问题描述：[LeedCode](https://leetcode-cn.com/problems/shortest-path-in-binary-matrix/)   
解决代码：
``` java
import javafx.util.Pair;

import java.util.LinkedList;
import java.util.Queue;

/**
 * 搜索算法：BFS（广度优先搜索）
 * leetcode:https://leetcode-cn.com/problems/shortest-path-in-binary-matrix/
 * 二进制矩阵中的最短路径
 * */
public class ShortestPathInBinaryMatrix {
    public int shortestPathBinaryMatrix(int[][] grid){
        //先判定数组不能为空，元素不能为空
        if(grid == null || grid.length == 0 || grid[0].length == 0){
            return -1;
        }
        //定义方向数组，共8个方向
        int[][] direction = {{0,-1},{-1,-1},{-1,0},{-1,1},{0,1},{1,1},{1,0},{1,-1}};
        int m = grid.length;
        int n = grid[0].length;
        //引入队列存路径上的元素
        Queue<Pair<Integer,Integer>> queue = new LinkedList<>();
        //先把grid[0][0]放到队列中，从[0][0]开始到[n-1][n-1]
        queue.add(new Pair<>(0,0));
        int pathLength = 0;
        while(!queue.isEmpty()){
            int size = queue.size();
            pathLength++;
            while(size > 0){
                size--;
                Pair<Integer,Integer> current = queue.poll();
                int currentKey = current.getKey();
                int currentValue = current.getValue();
                if(grid[currentKey][currentValue] == 1){
                    continue;
                }
                //这个是判定是否到右下角了，成功了
                if(currentKey == m-1 || currentValue == n-1){
                    return pathLength;
                }
                //如果可以走(为0),则标记一下，然后开始判断方向
                grid[currentKey][currentValue] = 1;
                for(int[] d : direction){
                    int newCurrentKey = currentKey + d[0];
                    int newCurrentValue = currentValue + d[1];
                    //判定往一个方向走一步，不超出边界
                    if(newCurrentKey < 0 || newCurrentKey >= m || newCurrentValue < 0 || newCurrentValue >= n){
                        continue;
                    }
                    queue.add(new Pair<>(newCurrentKey,newCurrentValue));
                }
            }
        }
        return -1;
    }
}
```

# 二、DFS
