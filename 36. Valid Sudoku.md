#<center>一天一道LeetCode</center>
>本系列文章已全部上传至我的github，地址：https://github.com/Zeecoders/LeetCode
>欢迎转载，转载请注明出处
##（一）题目
>Determine if a Sudoku is valid, according to: Sudoku Puzzles - The Rules.

>The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

>A partially filled sudoku which is valid.

##（二）解题
判断一个数独有效，从三个方面检查：
1、每一行包含1~9，且无重复
2、每一列包含1~9，且无重复
3、每一个3*3矩阵中包含1~9，切勿重复
```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int row[9][9] = {0};//每一行的检验矩阵
        int col[9][9] = {0};//每一列的检验矩阵
        int cross[9][9] = {0};//每一个3*3矩阵的检验矩阵
        for(int i = 0;i < 9;i++)
        {
            for(int j = 0 ; j < 9 ;j++)
            {
                int num = board[i][j] - '1';
                if(board[i][j]!='.')
                {
                    if(row[i][num]++) rturn false;//第i行出现num数字，如果为0，则标记为1，如果非零代表重复
                    if(col[j][num]++) return false;//如上
                    if(cross[i/3*3+j/3][num]++) return false;//将数独分为9个3*3矩阵，第i/3*3+j/3个矩阵出现num数字，其他如上
                }
            }
        }
        return true;
    }
};
```

