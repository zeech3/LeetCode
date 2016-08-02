#<center>一天一道LeetCode系列</center>
##（一）题目
>You are given an n x n 2D matrix representing an image.

>Rotate the image by 90 degrees (clockwise).

>Follow up:
>Could you do this in-place?

##（二）解题

90度旋转图像，我们不难看出$$matrix[i][j] = tmp[j][n-i-1]\quad \quad注:tmp=matrix$$经过这样的变换后，图像就旋转了90度。

```cpp


class Solution {

public:

    void rotate(vector<vector<int>>& matrix) {

        int n = matrix.size()-1;

        vector<vector<int>> tmp = matrix;//深拷贝

        for(int i = 0 ; i< n+1; i++)

        {

            for(int j = 0 ; j < n+1 ; j++)

            {

                matrix[j][n-i] = tmp[i][j];//赋值转换

            }

        }

    }

};

```
网上还有一种解法去先转置在对称变换。代码如下：

```cpp

class Solution {

public:

    void rotate(vector<vector<int> > &matrix) {

        int dim = matrix.size();

        int temp = 0;

        for (int i = 0; i < dim; ++i) { //先转置

            for (int j = i+1; j < dim; ++j) {

                temp = matrix[i][j];

                matrix[i][j] = matrix[j][i];

                matrix[j][i] = temp;

            }

        }

        for (int i = 0; i < dim/2; ++i) { //然后对称变换

            for (int j = 0; j < dim; ++j) {

                temp = matrix[j][i];

                matrix[j][i] = matrix[j][dim - i -1];

                matrix[j][dim - i -1] = temp;

            }

        }

    }

};

```