#<center>一天一道LeetCode系列<center/>
###（一）题目

> Given a string S, find the longest palindromic substring in S. You may
> assume that the maximum length of S is 1000, and there exists one
> unique longest palindromic substring.

题意：求一个字符串的最长回文字串。

###（二）解题
####1.中心扩展法
看到这个题首先想到的就是中心扩展法，遍历每一个字符，然后以该字符为中心向四周扩展，这种方法的时间复杂度为O（N^2），但是需要注意的是，奇数和偶数回文字符串需要区别对待，如aba和abba都是回文字符串。
```
class Solution {
public:
    string longestPalindrome(string s) {
        int max1=0;//奇数最长子串
        int max2=0;//偶数最长子串
        int idx1=0;//奇数最长子串的中心字符
        int idx2=0;//偶数最长子串的中心字符
        string result;
        for(int i = 0 ; i < s.length() ; ++i)
        {
            int j = i;
            int z = i;
            int count1=0;
            int count2=0;
            //计算奇数最长回文字符串
            while((++z<s.length()) && (--j>=0) && (s[z] == s[j]))
            {
                count1+=2;
                if(count1 > max1) 
                {
                    max1=count1;
                    idx1 = i;
                }
            } 
            //计算偶数最长回文字符串
            j = i;
            z = i+1;
            while((z<s.length()) && (j>=0) &&(s[z] == s[j]))
            {
                count2+=2;
                if(count2 > max2) 
                {
                    max2=count2;
                    idx2 = i;
                }
                z++;
                j--;
            }
        }
        if(max1+1>max2) result = s.substr(idx1-max1/2,max1+1);
        else result = s.substr(idx2-max2/2+1,max2);
        return result;
    }
};
```
####2.中心扩展法的优化
区分奇数和偶数显得程序比较臃肿，我们可以利用“改造“字符串来避免这种情况。如aba改成#a#b#a#，abba改成#a#b#b#a，这样就不用区分奇偶了。
```
class Solution {
public:
    string longestPalindrome(string s) {
        int max=0;
        int idx=0;
        string temp[2005];
        //改造字符串
        int j = 0;
        for(int i = 0; i < s.length() ; ++i)
        {
            temp[j++] = '#';
            temp[j++] = s[i];
        }
        temp[j++] = '#';
        temp[j] = '\0';
        for(int i = 0 ; i <2*s.length()+1 ; ++i)
        {
            int j = i;
            int z = i;
            int count=0;
            //计算奇数最长回文字符串
            while((++z<(2*s.length()+1)) && (--j>=0) && (temp[z] == temp[j]))
            {
                count++;
                if(count > max) 
                {
                    max=count;
                    idx = i;
                }
            } 
           
        }
        return s.substr((idx-max)/2,max);
    }
};
```
####3.动态规划法
DP算法的思想就是记录每一个回文子串的位置，在每一次判断是否为回文子串的时候先判断它的子串是不是回文，例如，用map[i][j]记录i到j为回文数组，如果这个时候s[i-1]==s[j+1]，那么就能在O(1)时间内判断[i-1,j+1]是否为回文了。
动态规划法的时间复杂度为O（n^2）.
```
class Solution {
public:
    string longestPalindrome(string s) {
        int len = s.length();
        int idx = 0;//记录最长回文字符的开始处
        int max = 1;//记录最长回文字符的长度
        int map[1000][1000] = {0};//记录i到j是否为回文子串
        for(int i = 0 ; i < len ; ++i)
        {
            map[i][i] = 1;//初始化长度为1的回文子串
        }
        for(int i = 0 ; i < len ; ++i)
        {
            if(s[i] == s[i+1])//初始化长度为2的子串
            {
                map[i][i+1] = 1;
                idx = i;
                max = 2;
            }
        }
        
        for(int plen = 3 ; plen <= len ; plen++)//从长度为3开始算起
        {//plen代表当前判断的回文子串的长度
            for(int j = 0 ; j < len - plen +1 ; j++)
            {
                int z = plen+j-1;//z为回文子串的尾序号
                if (s[j] == s[z] && map[j+1][z-1]) {
                //O（1）时间内判断j到z是否回文
                    map[j][z] = 1;
                    idx = j;
                    max = plen;    
                }
            }
        }
        return s.substr(idx,max);//返回子串
    }
};
```
####4.经典的Manacher算法，O（n）复杂度
算法步骤：
step1：跟解法2一样，改造字符串：
<center><font size=6>abba  -->  $#a#b#b#a#</font>     
<font color=red>注：加'$'是为了避免处理越界问题</font></center>
step2：用p[i]记录以i为中心点的回文字符串长度
<center>改造后的字符串：<font size=6>$#a#b#b#a#</font> 
p[]数组的值：<font size=6>121242121</font></center>
<center><font color=red>注：p[i]-1 = 源字符串中回文子串长度</font></center>
step3：利用DP的思想来求解p[]
<center>利用中心扩展法求以i为中心的最长回文串
<center><font size=4>`while(i+p[i] < temps.length() && temps[i-p[i]] == temps[i+p[i]]) p[i]++;`</font> 
利用p[]，mx，id记录的已有回文字符串的长度来避免大量重复的匹配
<font size=4>`if(mx > i)  p[i] = p[2*id-i] < (mx-i) ? p[2*id-i]:(mx-i);`</font></center>
<center><font color=red>注：p[2*id-i]为i关于j对称的点的回文串长度</font>
<font color=red>mx为i之前的回文串延伸到右边的最长位置，id为该回文串的中间值</font></center>
```
class Solution {
public:
    string longestPalindrome(string s) {
        string temps;
    	temps+="$#";//加$是为了避免处理越界情况，减小时间复杂度
    	for(int i = 0 ; i < s.length() ; ++i)//
    	{
    		temps+=s[i];
    		temps+="#";
    	}
    	int *p = new int[temps.length()];//p[i]记录以i为中心的回文串长度
    	memset(p, 0, sizeof(p));
    
    	int max = 0,idx = 0;//max记录最长回文串的长度，idx记录最长回文串的中心位置
    	int mx = 0,id = 0;//mx记录i之前的最长回文串延伸到最右边的位置，id记录该字符串的中心位置
    	for(int i = 1; i < temps.length() ; ++i)
    	{
    		if(mx > i)
    		{
    			p[i] = p[2*id-i] < (mx-i) ? p[2*id-i]:(mx-i);
    		}
    		else
    			p[i] = 1;
    
    		while(i+p[i] < temps.length() && temps[i-p[i]] == temps[i+p[i]]) 
    		{
    			p[i]++;
    		}
    		if(i+p[i]>mx)
    		{
    			id = i;
    			mx = i+p[i];
    			if(p[i]>max)
    			{
    				max = p[i];
    				idx = id;
    			}
    		}
    	}
    	max--;
        return s.substr((idx-max)/2,max);
    }
};
```
该算法的时间复杂度为O（n）。


以上代码在LeetCode中均Accepted。