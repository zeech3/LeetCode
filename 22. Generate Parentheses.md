#<center>一天一道LeetCode</center>
##（一）题目

> Given n pairs of parentheses, write a function to generate all
> combinations of well-formed parentheses.
> 
> For example, given n = 3, a solution set is:
> 
>> "((()))", "(()())", "(())()", "()(())", "()()()"
##（二）解题
在[ 【一天一道LeetCode】#20. Valid Parentheses](http://blog.csdn.net/terence1212/article/details/51175915)一文中提到怎么判断该组括号有效，另外在[【一天一道LeetCode】#17. Letter Combinations of a Phone Number](http://blog.csdn.net/terence1212/article/details/51153263)一文中用到回溯法。本题结合这两题的思路来解决。
假设在位置k之后，如果'('的数量还有剩余则可以继续添加；那么要添加')'，则必须满足其剩余的数量大于0且比'('剩余的数量大，才可以添加，否则就不是一个有效的括号组。

```
class Solution {
public:
    vector<string> ret;
    vector<string> generateParenthesis(int n) {
        string str;
        generate(str , n , n);
        return ret;
    }
    void generate(string str , int m , int n)
    {
        if(m==0)//
        {
	        while(n--) str+=')';//如果‘（’没有剩余的了，就直接把剩余的')'加上
            ret.push_back(str);
            return;
        }
        if(m>0)//如果‘（’剩余，可以继续添加'('
        {
            generate(str+'(',m-1,n);
        }
        if(m<n&&n>0)//如果m<n且n>0，可以继续添加')'
        {
            generate(str+')',m,n-1);
        }
    }
};
```