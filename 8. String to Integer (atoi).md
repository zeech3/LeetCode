#<center>一天一道LeetCode系列</center>
##（一）题目

> Implement atoi to convert a string to an integer.
> 
> Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.
> 
> Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.
> 
> Update (2015-02-10): The signature of the C++ function had been updated. If you still see your function signature accepts a const char* argument, please click the reload button  to reset your code definition.

##（二）解题
分析特殊情况：
1、字符前面有空格，“       010”
2、数字前或者中间出现了其他的字符“b123”，“   -012b12123”
3、数字越界，int是-2147483648到2147483647
4、最奇葩的+-2，我觉得应该输出-2，可是leetcode上显示输出0。
```
class Solution {
public:
    int myAtoi(string str) {
        long lresult=0;
        int i = 0;
        int max=2147483647;
        int min=-2147483648;
        bool isNegetive  = false;
        while(str[i] != '\0' && str[i] ==' ') i++;//判断前面是空格的情况
        if(str[i] == '-') {isNegetive = true;i++;}//判断正负
        else if(str[i] == '+'){i++;}
        
        while(i<str.length())
        {
            if(str[i]>='0' && str[i]<='9')
            {
                lresult*=10;
                lresult+=(str[i] - '0');
                i++;
            }
            else break;//出现其他字符干扰则退出循环
            //检查越界情况
            long lresult_temp = (isNegetive == true) ?-lresult:lresult;
            if(!isNegetive&&lresult_temp>=max) return max;
            if(isNegetive&&lresult_temp<=min) return min;
        }
        return (isNegetive == true) ?-lresult:lresult;//输出结果
        
    }
};
```
感觉做这道题还是自己考虑的情况不够多，总是遗漏了一些特殊情况。