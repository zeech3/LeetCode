#<center>一天一道LeetCode</center>

>本系列文章已全部上传至我的github，地址：[ZeeCoder‘s Github](https://github.com/Zeecoders/LeetCode)

>欢迎大家关注我的新浪微博，[我的新浪微博](http://weibo.com/zc463717263?is_all=1)
>
>欢迎转载，转载请注明出处

##（一）题目

>Validate if a given string is numeric.

>Some examples:
>"0" => true
>" 0.1 " => true
>"abc" => false
>"1 a" => false
>"2e10" => true

>Note: It is intended for the problem statement to be ambiguous. You should gather all requirements up front >before implementing one.
>Update (2015-02-10):
>The signature of the C++ function had been updated. If you still see your function signature accepts a const >char * argument, please click the reload button  to reset your code definition.
##（二）解题
题目大意：判断一个string数是否为有效数
大致从以下三点考虑这个问题：
1、全为数字
2、存在有且仅有一个’e‘，这个时候需要判断前后的数字有效，如4e+，.e1
3、存在有些仅有一个'.'，注意指数不能为小数
做题时没有考虑到的特殊情况：
“e”，“4e+”，“.e1”
```cpp
class Solution {
public:
    bool isNumber(string s) {
        int len = s.length();
        if(len == 0) return false;
        //剔除前面的空格
        int st = 0 ;
        while(st<len&&s[st] == ' ') st++;
        int ed = len-1;
        //剔除后面的空格
        while(ed>=0&&s[ed] == ' ') ed--;
        if(st>ed) return false;//如果全是空格就返回false
        //符号
        if(s[st]=='+'||s[st]=='-') st++;
        //标志.和e的位置
        int hase = -1;
        int hasdot =-1;
        //开始循环
        for(int i =st ; i <= ed ;)
        {
            if(s[i]>='0'&&s[i]<='9') i++;
            else if(s[i]=='e')
            {
                if(hase==-1) hase = i;//只能出现一个e
                else return false;
                if(i==st||i==ed) return false;//e在最前面或最后面返回false
                i++;
                if(s[i]=='+'||s[i]=='-') i++;//考虑指数带有符号
                if(i>ed) return false;//指数非法，如10e+
            }
            else if(s[i]=='.')
            {
                if(hasdot==-1) hasdot = i;//只能有一个.
                else return false;
                i++;
                if(ed-st==0) return false;//string为“.”的特殊情况
            }
            else return false;
        }
        if(hase!=-1&&hasdot!=-1){//判断e前面的数字有效
            if(hase<hasdot) return  false;//指数不能为小数
            if(hasdot==st&&hase-hasdot==1) return false;//“.e1”的特殊情况，e前面数要有效
        }
        return true;
    }
};
```