#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

>For example,
>Given the following matrix:

>>[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]


>You should return [1,2,3,6,9,8,7,4,5].

##（二）解题
相当于顺时针打印矩阵。我想到的方法就是一圈一圈的打印，每一圈的起点分别是(0,0),(1,1).....，那么退出循环打印的条件是什么呢？
我们可以分析3*3的矩阵有两圈，4*4的矩阵有两圈，5*5的矩阵有三圈，6*6的矩阵有三圈.....
假设m*n的矩阵，起点位置为(ori,ori)，那么满足的条件为m>ori*2&&n>ori*2
具体思路见代码注释：
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> ret;
        if(matrix.size() ==0) return ret;//矩阵为空的时候直接返回
        int ori=0;//每一圈的起点
        int row = matrix.size();
        int col = matrix[0].size();
        int px=ori,py=ori;
        int i , j , x, y;
        while(row>ori*2 && col > ori*2)//退出循环的条件
        {
                bool flag1 = false, flag2 = false, flag3 = false;//整圈打印需要连续，如果发生某一个方向没打印就下面的就不需要判断了
    		for (i = px; i < col - px; i++)//从左往右
    		{
    			ret.push_back(matrix[py][i]);
    			flag1 = true;
    		}
    		px = i-1;//i越界了，应该减1
    		for (j = py+1; j < row - py && flag1; j++)//从上到下
    		{
    			ret.push_back(matrix[j][px]);
    			flag2 = true;
    		}
    		py = j-1;//同上
    		for (x = px-1; x >= ori&&flag2; x--)//从右往左
    		{
    			ret.push_back(matrix[py][x]);
    			flag3 = true;
    		}
    		px = x+1;//同上
    		for (y = py-1; y > ori &&flag3; y--)//从下到上
    		{
    			ret.push_back(matrix[y][px]);
    		}
    		px = ++ori;//更新起点x
    		py = ori;//更新起点y
        }
        return ret;
    }
};
```