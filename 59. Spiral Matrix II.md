#<center>一天一道LeetCode系列</center>
##（一）题目
>Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

>For example,
>Given n = 3,

>You should return the following matrix:

>[
 >[ 1, 2, 3 ],
 >[ 8, 9, 4 ],
 >[ 7, 6, 5 ]
>]
##（二）解题

思路参考：  [【一天一道LeetCode】#54. Spiral Matrix](http://blog.csdn.net/terence1212/article/details/51459045)

还是一样按圈赋值，每一圈的起点分别为（0，0），（1，1）.....

```cpp

class Solution {

public:

    vector<vector<int>> generateMatrix(int n) {

        vector<vector<int>> ret;

        if(n==0) return ret;

        for(int i = 0 ; i < n ; i++)

        {

            vector<int> tmp(n,0);

            ret.push_back(tmp);

        }

        int count = 0 ; 

        int px = 0 , py = 0;//初始值

        int start = 0;//每一圈的起点

        while(start<n/2)

        {

            int i;

            for(i = py ; i<n - start; i++) {//从左往右

                ret[px][i] = ++count;

            }

            py = i-1;

            for(i = px+1 ; i<n - start ; i++){//从上往下

                ret[i][py] = ++count;

            }

            px = i-1;

            for(i = py-1 ; i>=start ; i--){//从右往左

                ret[px][i] = ++count;

            }

            py = i+1;

            for(i = px-1 ; i>=start + 1 ; i--){//从下往上

                ret[i][py] = ++count;

            }

            start++;

            px = py = start;//下一圈

        }

        if(n%2==1) ret[px][py] =++count;//n为奇数的时候需要考虑中心值

        return ret;

    }

};

```