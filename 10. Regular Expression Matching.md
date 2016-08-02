# <center>一天一道LeetCode系列</center>

# （一）题目

> Implement regular expression matching with support for '.' and '*'.
>> '.' Matches any single character.
>> '*' Matches zero or more of the preceding element.
>> 
>> The matching should cover the entire input string (not partial).
>> 
>> The function prototype should be: bool isMatch(const char *s, const
>> char *p)
>> 
>> Some examples: 
>> isMatch("aa","a") → false 
>> isMatch("aa","aa") → true
>> isMatch("aaa","aa") → false 
>> isMatch("aa", "a*") → true 
>> isMatch("aa",".*") → true 
>> isMatch("ab", ".*") → true 
>> isMatch("aab", "c*a*b") → true
# （二）解题
本题的意思是实现正则表达式的判断函数。
> tips：评级为hard的题还真是难做！

考虑到aaaaaab和a*b,这种无法判断*的结束位置，需要用到动态规划来求解。
分为以下两种情况：
case 1：p[j+1] !='*'时，无论是是s[i] == p[j]还是p[j]=='.',状态转移方程均为dfs[i][j] = dfs[i+1][j+1];
case 2：p[j+1] == '*'时，这个时候就需要判断*匹配的结束位置。
```cpp
    while(*s == *p || *s != '\0' && *p == '.')
    {
        if(Match(s,p+2)) return true;
        s++;
    }
```
结束位置找到以后状态转移方程为：dfs[i][j] = dfs[i][j+2];
接下来看代码：
```cpp
    class Solution {
    public:
        bool isMatch(string s, string p) {
           Match((const char *)&s[0],(const char *)&p[0]);
        }
        bool Match(const char *s,const char *p)
        {
            if(*p == '\0') return *s == '\0';
            if(*(p+1) == '*')
            {
                while(*s == *p || *s != '\0' && *p == '.')
                {
                    if(Match(s,p+2)) return true;
                    s++;
                }
                return Match(s,p+2);
            }
            else
            {
                if(*s == *p ||*s != '\0' && *p == '.')
                {
                    return Match(s+1,p+1);
                }
                return false;
            }
        }
    };
```