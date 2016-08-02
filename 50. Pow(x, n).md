#<center>一天一道LeetCode系列</center>
##（一）题目
>Implement pow(x, n).
##（二）解题
题目很简单，实现x的n次方。
```cpp
/*
需要注意一下几点：
1.n==0时，返回值为1
2.x==1时，返回值为1；x==-1时，根据n的奇偶来判断
3.n==-2147483648，特殊情况，int的范围时-2147483648～2147483647,
*/
class Solution {

public:

    double myPow(double x, int n) {

        if(n==0||x==1) return 1;

        

        if(x==-1&&n%2==0) return 1;

        if(x==-1&&n%2==1) return -1;

        

        if(n==-2147483648) return 1.0/(x*myPow(x,2147483647));

        if(n<0) return 1.0/myPow(x,0-n);

        if(n%2==0) return myPow(x*x,n/2);

        else return myPow(x*x,n/2)*x;

    }

};



```