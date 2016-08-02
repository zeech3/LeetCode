#<center>一天一道LeetCode系列</center>
##（一）题目
>Divide two integers without using multiplication, division and mod operator.

>If it is overflow, return MAX_INT.

##（二）解题

这题看起来很简单，一开始想到的方法就是从0开始一次累加除数，一直到比被除数大为止，好无悬念，这样做的结果就是超时了。

用移位来实现除法效率就比较高了。具体思路可以参考二进制除法。下面举个例子来说明。

例如：10/2 即10010/10

第一步：1-10不够减，结果添0，左移位变成10

第二步：10-10够减，结果添1，余010，左移位0

第三步：0-10不够减，结果添0，左移一位变成01

第四步：1-10不够减，结果添0，左移一位变成10

第五步：10-10够减，结果添1，后面没有位了，运算完毕

10010 = 10 *01001 即 10 = 2 * 5。

那么按照这种思路，我们每次对除数进行移位，找到等于或小于被除数(dividend)的最大值(max)，判断移位次数k，结果```ret += 1<<k```,然后dividend-=max，依次循环，知道dividend小于除数就运算完毕了。

还是以10/2为例

第一步：对2移位，找到等于或小于10的最大值8，移位次数k=2，ret=4，dividend = 10-8=2；

第二步：对2移位，找到等于或小于2的最大值2，移位次数k=0，ret=4+1=5，dividend=0

运算完毕！

```cpp

class Solution {

public:

    int divide(int dividend, int divisor) {

        if(divisor == 0) return 2147483647;//限制除数不能为0

        long long absdividend = abs((long long)dividend);//定义long long类型是为了防止越界

        long long absdivisor = abs((long long)divisor);//求绝对值

        long long ret = 0;

        while(absdividend >= absdivisor)//循环条件被除数大于除数

        {

            long long count = 1;

            long long tmpdiv = absdivisor;//初始值为除数

            while(tmpdiv<=absdividend){//移位后判断

                count<<=1;

                tmpdiv<<=1;

            }//找到了小于或等于被除数的最大值

            absdividend-=(tmpdiv>>1);//注意此处最大值应为tmpdiv>>1

            ret +=(count>>1);//上面多左移了一次，这里右移回来

        }

        if((dividend>0&&divisor<0)||(dividend<0&&divisor>0)){//判断正负

            ret = 0-ret;

        }

        if(ret>2147483647 ||ret<-2147483648) return 2147483647;//判断越界

        return (int)ret;//强制转换成int后退出

    }

};

```