#<center>一天一道LeetCode</center>
##（一）题目

> Given a digit string, return all possible letter combinations that the number could represent.
> 
> A mapping of digit to letters (just like on the telephone buttons) is
> given below.
> ![这里写图片描述](http://img.blog.csdn.net/20160414162840341)
> 
> 
> 	> Input:Digit string "23" Output: ["ad", "ae", "af", "bd", "be", "bf",
> 	> "cd", "ce", "cf"].
##（二）解题
这题采用回溯法。
以23为例，2对应“abc” ，3对应“def。
第一步：a,b,c
第二部：ad，ae，af，bd，be，bf，cd ，ce，cf
回溯法的意思是，依次递归到最后，如果到最后了就回溯，继续递归。
算法的过程：
首先依次递归得到ad，到digits的长度了，回溯得到a
这下又可以递归了，得到ae，又到digits的长度了，再回溯到a
然后继续循环得到af，f到头了，a也到头了，轮到b上场了！
.......依次下去就把所有的情况都输出了！

```
class Solution {
public:
    string phoneStr[10] = {"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    string tmp;
    vector<string> result;
    vector<string> letterCombinations(string digits) {
        if(digits.length()==0) return result;
        dfs(digits , 0);
        return result;
    }
    void dfs(string &str , int idx)
    {
        if(idx == str.length())
        {
            result.push_back(tmp);//递归结束条件
            return;  
        }
        else
        {
            for(int i = 0 ; i < phoneStr[str[idx]-'0'].length() ; i++)
            {
                tmp = tmp.substr(0,idx);//回溯！
                tmp+=(phoneStr[str[idx]-'0'])[i];
                dfs(str,idx+1);
            }
        }
            
    }
};
```