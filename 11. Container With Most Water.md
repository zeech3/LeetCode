# <center>一天一道LeetCode系列</center>

##（一）题目

> Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
> 
> Note: You may not slant the container.

##（二）解题
题意：给定一组高度值，选取其中两个使得两者构成的容器的容量最大。
按照题意，一个双重循环可以很简单的解决问题，可是复杂度太高了，O(n^2)。
那么我们可以寻找O(n)的解法。
其实也比较简单，定义两个指针，分别指向头和尾，由于容易装水的容量是由小端决定，所以指针移动的准则就是小端指针移动。
只需要遍历一遍就能得到最大值。
```
class Solution {
public:
    int maxArea(vector<int>& height) {
        int i = 0;
        int j = height.size()-1;
        int max=0;
        while(j>i)
        {
            int con = 0;
            int min = height[i]>height[j]?height[j]:height[i];
            if(j==i+1){con = min;}
            else
                con = min *(j-i);
            if(height[i]>height[j])
            {
                j--;
            }
            else i++;
            if(con>max) max=con;
        }
        return max;
    }
};
```