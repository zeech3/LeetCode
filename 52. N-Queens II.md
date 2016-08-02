#<center>一天一道LeetCode系列</center>
##（一）题目
>Follow up for N-Queens problem.
![这里写图片描述](http://www.leetcode.com/wp-content/uploads/2012/03/8-queens.png)
>Now, instead outputting board configurations, return the total number of distinct solutions.

##（二）解题
具体思路参考[【一天一道LeetCode】#51. N-Queens](http://blog.csdn.net/terence1212/article/details/51435966)
```cpp
/*
与N-Queens不同的事，这题只要求输出摆放方式的个数，因此对程序只需要做小的改动
*/
class Solution {
public:
    int count = 0;//记录次数
    vector<pair<int, int>> queens;//存放已摆放的皇后的坐标值
    int totalNQueens(int n) {
        int *a = new int[n];//确保每一列只有一个皇后
        memset(a,0,n*sizeof(int));
        backtrc(a, 0, n);
        return count;
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
    void backtrc(int a[], int row, int n)//row确保每一行只有一个皇后
    {
        if (row == n)//如果摆放完n行，则退出
        {
            count++;//次数加1
            return;
        }
        for (int i = 0; i < n; i++)
        {
            if (a[i] == 0&&isValid(queens, row, i))//保证了同一行，同一列，同一对角线只有一个Q
            {
                a[i] = 1;
                queens.push_back(pair<int, int>(row, i));
                backtrc(a, row + 1, n);
                //回溯
                a[i] = 0;
                queens.pop_back();
            }
        }
    }
};
```