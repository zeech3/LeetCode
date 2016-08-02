#<center>一天一道LeetCode系列</center>
##（一）题目

> Given an integer, convert it to a roman numeral.
> 
> Input is guaranteed to be within the range from 1 to 3999.
##（二）解题
将整形数字转换成罗马数字
罗马数字共有七个，即I(1)，V(5)，X(10)，L(50)，C(100)，D(500)，M(1000)
举例：Ⅰ、Ⅱ、Ⅲ、Ⅳ、Ⅴ、Ⅵ、Ⅶ、Ⅷ、Ⅸ、Ⅹ、Ⅺ、Ⅻ表示1-11
代码：

```
class Solution {
public:
    string intToRoman(int num) {
        string str = "";
        string roman[8] = {"I","V","X","L","C","D","M"};
        int j=0;
        while(num)
        {
            int temp = num%10;
            string str_t ="";
            if(temp <4)
            {
                int count = temp;
                while(count--) str_t+=roman[j];
            }
            else if(temp==4)
            {
                str_t=roman[j];
                str_t+=roman[j+1];
            }
            else if(temp>=5&&temp<=8)
            {
                str_t+=roman[j+1];
                int count = temp-5;
                while(count--) str_t+=roman[j];
            }
            else if(temp==9)
            {
                str_t+=roman[j];
                str_t+=roman[j+2];
            }
            cout<<roman[j]<<endl;
            cout<<str_t<<endl;
            str =str_t+str;
            j=j+2;
            num = num/10;
        }
        return str;
    }
};
```
我这段代码看起来比较臃肿。看到网上的写法如beiyeqingteng博主的：

```
public class Solution {  
    public String intToRoman(int number) {  
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1 };  
        String[] numerals = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I" };  
        StringBuilder result = new StringBuilder();  
        for (int i = 0; i < values.length; i++) {  
            while (number >= values[i]) {  
                number -= values[i];  
                result.append(numerals[i]);  
            }  
        }  
        return result.toString();  
    }  
}  
```

看起来就简单多了。