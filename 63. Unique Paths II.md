#<center>一天一道LeetCode</center>

##（一）题目

>Follow up for "Unique Paths":

>Now consider if some obstacles are added to the grids. How many unique paths would there be?

>An obstacle and empty space is marked as 1 and 0 respectively in the grid.

>For example,

>There is one obstacle in the middle of a 3x3 grid as illustrated below.

>[

  >[0,0,0],

 > [0,1,0],

 > [0,0,0]

>]

>The total number of unique paths is 2.



##（二）解题

解题思路：参考上一篇博文[【一天一道LeetCode】#62. Unique Paths](http://blog.csdn.net/terence1212/article/details/51502144)

```

class Solution {

public:

    int dp[101][101];

    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {

        int row = obstacleGrid.size();

        int col = 0;

        if(row!=0) col = obstacleGrid[0].size();

        if(obstacleGrid[0][0]==1) return 0;//起始点不通则直接返回0

        for(int i = row-1 ; i>=0 ; i--)

            for(int j = col-1 ; j>=0 ; j--)

            {

                if(obstacleGrid[i][j]==1) dp[i][j] = 0;//代表此路不通

                else if(i==row-1&&j==col-1) dp[i][j] = 1;//规定终点的dp为1

                else dp[i][j] = dp[i+1][j]+dp[i][j+1];

            }

        return dp[0][0];

    }

```

