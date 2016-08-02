#<center>一天一道LeetCode系列</center>
##（一）题目

> Determine whether an integer is a palindrome. Do this without extra
> space.
> Some hints:
> Could negative integers be palindromes? (ie, -1)
> 
> If you are thinking of converting the integer to string, note the
> restriction of using extra space.
> 
> You could also try reversing an integer. However, if you have solved
> the problem "Reverse Integer", you know that the reversed integer
> might overflow. How would you handle such case?
> 
> There is a more generic way of solving this problem.

##（二）解题
题目需要判断一个整数是不是回文数。需要注意一下几点：、
1、负数不是回文数
2、回文数满足反转后与原数相等，在反转整数那一题里面提到需要考虑越界问题，所以需要将int转换成long来处理。
代码比较简单，如下：

```
class Solution {
public:
    bool isPalindrome(int x) {
        if(x<0) return false;
        else{
            long n = 0;
            long temp = x;//考虑到反过来越界
            long lx = x;
            while(temp)
            {
                n = n*10+temp%10;//反转int数
                temp = temp/10;
            }
            if(n==lx) return true; //与原数相等则返回true
            else return false;
        }
    }
};
```