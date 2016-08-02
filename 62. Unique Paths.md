#<center>一天一道LeetCode系列</center>
##（一）题目
>A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).
![这里写图片描述](http://leetcode.com/wp-content/uploads/2014/12/robot_maze.png)
>The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the >diagram below).

>How many possible unique paths are there?



>Above is a 3 x 7 grid. How many possible unique paths are there?

>Note: m and n will be at most 100.

##（二）解题

主要思想：对于i，j这一点来说，它到终点的路径数dp[i][j] = dp[i+1][j]+ dp[i][j+1]，这就是状态转移方程，然后利用动态规划来求解！

###递归版本


```cpp
class Solution {
public:
    int dp[101][101];//用来标记已经计算过的路径
    int uniquePaths(int m, int n) {
        dp[m-1][n-1] = 1;
        int ret = dfsPath(0,0,m-1,n-1);
        return ret;
    }
    int dfsPath(int pm,int pn,int m ,int n)
    {
        
        if(pm==m && pn==n) return 1 ;
        int down = 0;
        int right = 0;
        if(pm+1<=m) down = dp[pm+1][pn]==0?dfsPath(pm+1,pn,m,n):dp[pm+1][pn];//往下走的那一格到终点的路径数
        if(pn+1<=n) right = dp[pm][pn+1]==0?dfsPath(pm,pn+1,m,n):dp[pm][pn+1];//往右走的那一格到终点的路径数
        dp[pm][pn] = down+right;
        return dp[pm][pn];
    }
};
```
###非递归版本
```cpp
/*
提示：这个版本画个图可能会更好理解
*/
class Solution {
public:
    int uniquePaths(int m, int n) {
        int dp[101][101];
        for(int i = 0 ; i < m ; i++) dp[i][n-1] = 1;//首先初始化dp
        for(int i = 0 ; i < n ; i++) dp[m-1][i] = 1;
        if(m==1||n==1) return 1;//特殊情况
        for(int i = m-2 ; i>=0 ; i--)
            for(int j = n-2 ; j>=0 ; j--)
            {
                dp[i][j] = dp[i+1][j] + dp[i][j+1];//状态转移方程
            }
        return dp[0][0];
    }
};
```