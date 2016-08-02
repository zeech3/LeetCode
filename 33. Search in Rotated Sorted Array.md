#<center>一天一道LeetCode</center>

>本系列文章已全部上传至我的github，地址：
>https://github.com/Zeecoders/LeetCode
>欢迎转载，转载请注明出处

##（一）题目

>Suppose a sorted array is rotated at some pivot unknown to you beforehand.
>(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).
>You are given a target value to search. If found in the array return its index, otherwise return -1.
>You may assume no duplicate exists in the array.

##（二）解题

一个排好序的数组，经过一定的旋转之后得到新的数组，在这个新的数组中查找一个目标数。
那么，首先我们需要在旋转后的数组中找到原数组的起始点，并将数组分成两部分。
例如：4，5，6，7，0，1，2分为4，5，6，7和0，1，2
然后，确定目标数在哪一个部分，
最后，采用二分法来进行加速搜索！
具体看代码：
###未优化版本
```cpp
class Solution {
public:

    int search(vector<int>& nums, int target) {

        int len = nums.size();

        int i = 0 ; 

        int j = len-1;

        int p = 0 ;

        while(p+1<len&&nums[p]<nums[p+1]) p++;//找出第一个破坏升序的数即为旋转中心

        if(nums[0]<=target) j=p;//确定被查找的数在哪个部分

        else if(nums[len-1]>=target) i=p+1;

        while(i<=j)//二分搜索

        {

            int mid = (i+j)/2;

            if(nums[mid] == target) return mid;

            else if(nums[mid] >target) j= mid-1;

            else i = mid+1;

        }

        return -1;//未找到则返回-1

    }

};

```

AC之后一看运行时间8ms，看来代码还有待优化，于是在查找旋转中心的方法上进行优化，采用二分法进行搜索旋转中心。

###优化版本

```cpp

class Solution {

public:

    int search(vector<int>& nums, int target) {

    	int len = nums.size();

    	int i = 0;

    	int j = len - 1;

    	int p = 0;

    	bool isfind = false;

    	if (nums[0]>nums[len-1])//如果进行了旋转

    	{

    		while (i < j)//二分搜索旋转中心

    		{

    			if (i == j - 1) {

    				isfind = true;

    				break;

    			}

    			int mid = (i + j) / 2;

    			if (nums[i] < nums[mid]) i = mid;

    			if (nums[j] > nums[mid]) j = mid;

    		}

    	}

    	if (isfind)//找到了旋转中心

    	{

    		if (nums[0] <= target) { j = i; i = 0; }

    		if (nums[len - 1] >= target) { i = j; j = len - 1;}

    	}

    	while (i<=j)二分搜索目标数

    	{

    		int mid = (i + j) / 2;

    		if (nums[mid] == target) return mid;

    		else if (nums[mid] >target) j = mid-1;

    		else i = mid+1;

    	}

    	return -1;

    }

};

```

优化后的版本运行时间4ms，快了一半！