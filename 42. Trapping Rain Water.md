#<center>一天一道LeetCode系列</center>
##（一）题目
>Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much >water it is able to trap after raining.

>For example, 
>Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.

>![这里写图片描述](http://img.blog.csdn.net/20160506155005896)

>The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. Thanks Marcos for contributing this image!

##（二）解题

题目需要求的是矩阵作为容器能盛多少体积的水。
方法可以参考我的这篇博客：[【一天一道LeetCode】#11Container With Most Water](http://blog.csdn.net/terence1212/article/details/51079744)
```cpp
/*
思路：考虑到所盛的水取决于容器两端中小的那一端。因此用两个指针，分别指向头和尾，依次向中间移动。
1.如果左边小，则左边向右移动一格，这个时候需要判断向右移动一格后
①如果高度大于原来的就表示盛不下水
②如果小于原来的则表示有凹下去的部分，这个时候计算高度差就代表能盛多少水。(右边比左边高，可以保证右边不溢出)
2.如果右边小，则右边向左移动一格，这个时候同1一样判断。
*/
class Solution {
public:
    int trap(vector<int>& height) {
        if(height.size()<=2) return 0;
        int ret = 0;
        int l = 0;
        int r = height.size()-1;
        int left = height[0];
        int right = height[r];
        while(l<r)
        {
            if(left<=right)
            {
                l++;
                if(height[l]>=left)
                {
                    left = height[l];
                }
                else ret+=(left-height[l]);
            }
            else
            {
                r--;
                if(height[r]>=right)
                {
                    right = height[r];
                }
                else ret +=(right-height[r]);
            }
        }
        return ret;
    }
};

```