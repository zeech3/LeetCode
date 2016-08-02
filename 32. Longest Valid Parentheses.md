#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

>For "(()", the longest valid parentheses substring is "()", which has length = 2.

>Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.


##（二）解题
```cpp
/*
stack法思想：和Valid Parentheses一样，用stack来解决，只不过栈中记录的是每个‘（’的下标
1.首先在栈里面压入初始值-1(初始匹配失败的下标)， 如果是‘（’就直接把‘（’的下标压进栈
2. 如果是‘）’开始判断
(1) 如果此刻栈的大小大于1，则将栈顶元素弹出，将下标减去当前的栈顶元素即为当前有效串的长度
(2) 如果此刻栈的大小小于等于1，则代表匹配失败，更新目前匹配失败的下标。
*/
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> stmp;
        stmp.push(-1);
        int max = 0;
        for(int i = 0 ; i < s.length() ; i++){
            if(s[i] == '(')
            {
                stmp.push(i);
            }
            else
            {
                if(stmp.size()>1)
                {
                    stmp.pop();
                    int len = i - stmp.top();
                    max = max>len?max:len;
                }
                else
                {
                    stmp.pop();
                    stmp.push(i);
                }
            }
        }
        return max;
    }
};
```