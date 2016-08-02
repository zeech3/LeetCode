#<center>一天一道LeetCode系列</center>
##（一）题目
>Implement wildcard pattern matching with support for '?' and '*'.
>>'?' Matches any single character.
>>'*' Matches any sequence of characters (including the empty sequence).
>>The matching should cover the entire input string (not partial).
>>The function prototype should be:
>>bool isMatch(const char *s, const char *p)
>>Some examples:
>>isMatch("aa","a") → false
>>isMatch("aa","aa") → true
>>isMatch("aaa","aa") → false
>>isMatch("aa", "*") → true
>>isMatch("aa", "a*") → true
>>isMatch("ab", "?*") → true
>>isMatch("aab", "c*a*b") → false
##（二）解题
1、递归解法
看到这题首先想到的是之前做的正则表达式那题[【一天一道LeetCode】#10. Regular Expression Matching](http://blog.csdn.net/terence1212/article/details/51185042)，于是想都没有想，按照之前的方法，很明显，超时了。
```cpp
/*
1.如果s[i]==p[j]||p[j] == '?' ,则i++，j++
2.如果p[j] =='*'，就判断s[i]和p[j+1]以后的字串能否匹配上，如果能则返回true，如果不能则i++
*/
class Solution {
public:
    bool isMatch(string s, string p) {
        int i = 0;
        int j = 0;
        while(i<s.length()&&j<p.length())
        {
            if(s[i] == p[j] || p[j] == '?')
            {
                i++;
                j++;
            }
            else if(p[j] == '*')
            {
                if(j==p.length()-1) return true;
                else
                {
                    while(i<s.length()&&s[i]!=p[j+1]) i++;
                    if(i==s.length()) return false;
                    else{
                        string tmps = s.substr(i,s.length());
                        string tmpp = p.substr(j+1,p.length());
                        if(isMatch(tmps,tmpp)) return true;//判断后面的能否匹配
                        else i++;
                    }
                }
            }
            else break;
        }
        if(i==s.length()&&j==p.length()) return true;
        else return false;
    }
};
```
2、 回溯法
首先我们看一个例子caabbbbc和c*ab*c，后者可以写成c......ab.....c，这样一来我们只要在两个c之间找到ab就能匹配上了，
于是当碰到*的时候就记录下此时的spre = i和ppre = ++j，然后比较s[++i]和p[++j]，如果不等就回溯到i=++spre，j=ppre ,
如果碰到下一个‘*’ ， 就代表ab已经匹配完成了，更新spre和ppre，循环比较，直到字符串尾。 
这就是本解法主要思想。
```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int i = 0,j = 0;
        int slen = s.length();
        int plen = p.length();
        int spre = 0 , ppre = 0;//回溯法
        bool isflag = false;
        while(i<slen)
        {
            if(s[i]==p[j] || p[j]=='?')
            {
                i++;
                j++;
            }
            else if(p[j] == '*')
            {
                ppre = ++j;//记录*位置，一遍回溯匹配
                spre = i;
                isflag = true;//代表前面出现过‘*’
            }
            else 
            {
                if(isflag)//s[i] != p[j]而且p[j]！='?'，匹配失败，回溯
                {
                    i = ++spre;
                    j = ppre;
                }
                else return false;//如果前面没有‘*’，则代表匹配失败，返回false
            }
        }
        while(p[j]=='*') j++;//防止出现p末尾都是‘*’的特殊情况
        if(j==plen) return true;
        else return false;
    }
};
```