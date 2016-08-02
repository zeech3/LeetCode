#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

>If the last word does not exist, return 0.

>Note: A word is defined as a character sequence consists of non-space characters only.

>For example, 
>Given s = "Hello World",
>return 5.

##（二）解题
题目比较简单，从尾向头找，第一个不为空格的字母，然后再继续找遇到空格为止。纪录单词长度。

```cpp

class Solution {

public:

    int lengthOfLastWord(string s) {

        if(s.length() == 0) return 0;

        int count = 0;

        int i = s.length()-1;

        while(s[i]==' ') i--;//忽略前面的空格

        while(i>=0&&s[i]!=' ') //当为字母的时候计算长度，为空格就退出循环

        {

            count++;

            i--;

        }

        return count;

    }

};

```