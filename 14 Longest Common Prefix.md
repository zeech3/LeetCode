#<center>一天一道LeetCode系列</center>
##（一）题目：

> Write a function to find the longest common prefix string amongst an
> array of strings.
##（二）题意
求一组字符串中的最长前缀字符串。
举例：字符串组：abc，ab，abdef，abws 最长前缀字符串：ab

我的解法是先求出这组字符串中最短的，然后依次匹配，遇到不同的就退出。

```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.size()==0) return "";
        if(strs.size()==1) return strs[0];
        
        string minstr=strs[0];
        string compre="";
        int minlen=strs[0].length();
        for(int i = 0 ; i<strs.size() ; i++)//求出最短的字符串
        {
            int len = strs[i].length();
            if(len<minlen)
            {
                minlen = len;
                minstr = strs[i];
            } 
        }
        for(int i = 0 ; i < minlen ; i++)
        {
            int j = 0;
            int count = 0;
            while(j < strs.size()) 
            {
                string temp = strs[j];//依次匹配
                if(temp[i] == minstr[i])
                {
                    count++;
                }
                j++;
            }
            if(count == strs.size())
            {
                compre+=minstr[i];
            }
            else break;//碰到不相同的就退出
        }
        return compre;
    }
};
```