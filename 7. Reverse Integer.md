#<center>一天一道LeetCode系列</center>
##（一）题目

> Reverse digits of an integer.
> Example1: x = 123, return 321
>  Example2: x = -123, return -321

##（二）解题
这题看上去很简单，动笔一挥之下，写出如下代码：

```
class Solution {
public:
    int reverse(int x) {
        bool flag = false;
        if(x<0) {
            x=-k;
            flag = true;
        } 
        long result=0;
        while(x!=0)
        {
            result*=10;
            result+=x%10;
            x=x/10;
        }
        return flag==true ?-result:result;
    }
};
```
满心以为一步就能Accepted。没想到直接wrong answer！！
1534236469反过来9646324351超过了int的最大值，于是修改代码：
```
class Solution {
public:
    int reverse(int x) {
        long k = x;
        bool flag = false;
        if(k<0) {
            k=-k;
            flag = true;
        } 
        long result=0;
        while(k!=0)
        {
            result*=10;
            result+=k%10;
            k=k/10;
        }
        if(result>2147483648||result<-2147483647) return 0;//判断越界没有
        else return flag==true ?(int)-result:(int)result;//结果判断正负输出
    }
};
```
这下能accepted了！果然越是看起来简单的题目越需要细节处理！