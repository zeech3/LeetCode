#<center>一天一道LeetCode系列</center>
##（一）题目

> The string "PAYPALISHIRING" is written in a zigzag pattern on a given
> number of rows like this: (you may want to display this pattern in a
> fixed font for better legibility)
> 
> P   A   H   N A P L S I I G Y   I   R And then read line by line:
> "PAHNAPLSIIGYIR" Write the code that will take a string and make this
> conversion given a number of rows:
> 
> string convert(string text, int nRows); convert("PAYPALISHIRING", 3)
> should return "PAHNAPLSIIGYIR".

题意：
![这里写图片描述](http://img.blog.csdn.net/20160403162702312)

##（二）解题

已知输入条件：初始string s和numRows。可以得出循环间隔gap =  2*numRows-2。
统计规律：
 - 第0行  从j=0开始，间距gap，取s[j]
 - 第1~numRows-2行  从j=1开始，间距`gap=(j%gap)<numRows?(gap-2(j%gap)):(2*gap-2(j%gap))`，取s[j]
 - 第numRows-1行，间距gap，取s[j]
 代码如下：
```
class Solution {
public:
    string convert(string s, int numRows) {
        string result;
        int gap=2*numRows-2; //初始化gap
        if(numRows == 1) return s;//rows为1，直接返回
        for(int i = 0 ; i < numRows ; i++)
        {
            int j = i ;
            bool flag = true;
            if(i == 0 || i == numRows-1)//如果第0行或最后一行
            {
                int j = i;
                while(j<s.length()) 
                {
                    result+=s[j];
                    j += gap;//间距为gap
                }
            }
            else{
                int j = i;
                while(j<s.length()){
                    result+=s[j];
                    j += (j%gap)<numRows?(gap-2*(j%gap)):(2*gap-2*(j%gap));
                }
            }
        }
        return result;
    }
};
```