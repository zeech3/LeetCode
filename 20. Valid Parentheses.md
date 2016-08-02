#<center>一天一道LeetCode系列</center>
##（一）题目

> Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
> 
> The brackets must close in the correct order, "()" and "()[]{}" are
> all valid but "(]" and "([)]" are not.
##（二）解题
本题的关键在于利用stack，想到了stack就不难写出代码了。
每次碰到（，{，[就压栈，碰到），}，]，就判断栈顶元素匹配上就出栈，匹配不上就返回false.
下面是Accepted的代码，复杂度为0（n）：

```
class Solution {
public:
    bool isValid(string s) {
        stack<char> tmp;
        for(int i = 0 ; i < s.length() ; i++)
        {
            if(s[i] == '(' || s[i] == '{' || s[i] == '[')
            {
                tmp.push(s[i]);
            }
            else if(s[i] == ')' || s[i] == '}' || s[i] == ']')
            {
                if(tmp.empty()) return false;
                switch(s[i])
                {
                case ')':
                    if(tmp.top() == '(') tmp.pop(); 
                    else return false;
                    break;
                case ']':
                    if(tmp.top() == '[') tmp.pop(); 
                    else return false;
                    break;
                case '}':
                    if(tmp.top() == '{') tmp.pop(); 
                    else return false;
                    break;
                }
            }
        }
        if(tmp.empty()) return true;
        else return false;
    }
};
```