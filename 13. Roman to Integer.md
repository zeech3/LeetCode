#<center>一天一道LeetCode系列</center>
##（一）题目

> Given a roman numeral, convert it to an integer.
> 
> Input is guaranteed to be within the range from 1 to 3999.

##（二）解题
和上一题相反，这题将罗马数字转换成整形数。
注意到 4，9，40，90,400,900这些特殊的数字的区别就不难写出代码了。
```
class Solution {
public:
    int romanToInt(string s) {
        int ret=0;
         for(auto iter = s.begin() ; iter!=s.end() ; ++iter)
         {
             if((iter+1)!=s.end() && tonum(*iter) < tonum(*(iter+1)))
                {
                    ret += tonum(*(iter+1))-tonum(*iter);
                    ++iter;
                }
             else 
                ret += tonum(*iter);
         }
         return ret;
    }
    
    int tonum(char ch)
    {
        switch(ch)
        {
            case 'I' : return 1;
            case 'V' : return 5;
            case 'X' : return 10;
            case 'L' : return 50;
            case 'C' : return 100;
            case 'D' : return 500;
            case 'M' : return 1000;
        }
    }
    
};
```