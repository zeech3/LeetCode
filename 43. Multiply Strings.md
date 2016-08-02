#<center>一天一道LeetCode系列</center>
##（一）题目
>Given two numbers represented as strings, return multiplication of the numbers as a string.

>>Note:
>>The numbers can be arbitrarily large and are non-negative.
>>Converting the input string to integer is NOT allowed.
>>You should NOT use internal library such as BigInteger.
##（二）解题
两个string代表的数字相乘，主要就是要求写出大数相乘的代码，具体看注释
```
/*
本题的思路主要是：num1的第i位和num2的第j位相乘等于乘积的第i+j位
m位数和n位数相乘的结果最大位m+n位！
1.为了便于理解，将两个string首先反转
2.两个for循环，从num1的0位开始，依次乘上num2的0-size位，注意考虑到进位的问题
3.对于结果ret，先反转，如果全为0，则直接返回0，否则去掉前面连续的0，即为最后的结果
*/
class Solution {
public:
    string multiply(string num1, string num2) {
        reverse(num1.begin(),num1.end());//反转num1
        reverse(num2.begin(),num2.end());//反转num2
        string ret(num1.size()+num2.size(),'0');
        for(int i = 0 ; i < num1.size() ; i++)
        {
            int carry = 0;//处理进位
            int j = 0;
            for(; j < num2.size() ; j++)
            {
                carry += (ret[i+j]-'0') + (num1[i]-'0')*(num2[j]-'0');
                ret[i+j] = ('0'+carry%10) ;
                carry /=10;
            }
            if(carry!=0)//处理最后的进位
            {
                ret[i+j] = ('0'+carry);    
            }
        }
       //对最后的字符串进行处理
        reverse(ret.begin(),ret.end());
        for(auto iter=ret.begin() ; iter!=ret.end() ; )
        {
            if(*iter == '0'&&ret.size()>1) iter = ret.erase(iter);//如果为‘0’则删除
            else break;//第一位不为‘0’的数就退出
        }
        return ret;
    }
};
```

