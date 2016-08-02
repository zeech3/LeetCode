#<center>一天一道LeetCode系列</center>
##（一）题目
>The count-and-say sequence is the sequence of integers beginning as follows:
>1, 11, 21, 1211, 111221, ...

>1 is read off as "one 1" or 11.
>11 is read off as "two 1s" or 21.
>21 is read off as "one 2, then one 1" or 1211.

>Given an integer n, generate the nth sequence.

>Note: The sequence of integers will be represented as a string.

##（二）解题
```cpp
/*
首先初始化字符串为1，对应一个1，读成11
字符串更新为11，对应两个1，读成21
字符串更新为21，对应1个2一个1，读成1211
....
依次进行n次则得到最后的字符串
*/
class Solution {
public:
    string countAndSay(int n) {
        string str = "1";
    	while(--n)
    	{
    		string ret;
    		for (int i = 0; i < str.length(); ) {
    			int count = 0;
    			while (i < str.length() && str[i] == str[i + 1]) {
    				count++;
    				i++;
    			}
    			ret += ('1' + count);
    			ret += str[i];
    			i++;
    		}
    		str = ret;
    	}
    	return str;
    }
};
```