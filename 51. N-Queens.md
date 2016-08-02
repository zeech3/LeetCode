#<center>一天一道LeetCode系列</center>
##（一）题目
>The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.
>![这里写图片描述](http://www.leetcode.com/wp-content/uploads/2012/03/8-queens.png)
>Given an integer n, return all distinct solutions to the n-queens puzzle.
>Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space >respectively.
>For example,
>There exist two distinct solutions to the 4-queens puzzle:
>[
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],
> ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]
##（二）解题
不玩国际象棋还真不知道这题的规则。百度了好久才明白。
主要有以下三个：
+ 同一行上只能有一个皇后
+ 同一列上只能有一个皇后
+ 两个皇后之间不能处在同一条对角线上
具体解法看代码：
```cpp
/*
首先利用一个数row和数组a[i]确保每一行每一列只有一个皇后
然后利用一个vector存储已摆放皇后的位置坐标，每摆一个皇后就与已摆放的皇后进行比较，如果在一条对角线上就不能摆
*/
class Solution {
public:
    vector<vector<string>> ret;
    vector<pair<int, int>> queens;//存放已摆放的皇后的坐标值
    vector<vector<string>> solveNQueens(int n) {
        int *a = new int[n];//确保每一列只有一个皇后
    	memset(a,0,n*sizeof(int));
    	vector<string> res;
    	backtrc(res, a, 0, n);
    	return ret;
    }
    bool isValid(vector<pair<int,int>> queens , int row,int col)//
    {
    	if (queens.empty()) return true;
    	for (int i = 0; i < queens.size();i++)
    	{
    		if (abs(row- queens[i].first) == abs(col-queens[i].second))
    		{
    			return false;
    		}
    	}
    	return true;
    }
    void backtrc(vector<string> res, int a[], int row, int n)//row确保每一行只有一个皇后
    {
    	if (row == n)//如果摆放完n行，则退出
    	{
    		ret.push_back(res);
    		return;
    	}
    	for (int i = 0; i < n; i++)
    	{
    		if (a[i] == 0&&isValid(queens, row, i))//保证了同一行，同一列，同一对角线只有一个Q
    		{
    			a[i] = 1;
    			string tmp(n, '.');
    			tmp[i] = 'Q';
    			res.push_back(tmp);
    			queens.push_back(pair<int, int>(row, i));
    			backtrc(res, a, row + 1, n);
    			//回溯
    			a[i] = 0;
    			queens.pop_back();
    			res.pop_back();
    		}
    	}
    }
};
```

