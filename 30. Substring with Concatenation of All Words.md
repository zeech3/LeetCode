<font color = red>注：这道题之前跳过了，现在补回来<font>


----------


#<center>一天一道LeetCode系列</center>
##（一）题目
>You are given a string, s, and a list of words, words, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each >word in wordsexactly once and without any intervening characters.

>For example, given:
s: "barfoothefoobarman"
words: ["foo", "bar"]

>You should return the indices: [0,9].
(order does not matter).


##（二）解题
本题需要在s中找到一串子串，子串是words中的单词按一定顺序排列组成的。返回这个子串在s中的起始位置。
主要思路：由于要考虑words中的重复单词，需要用到multiset，加快查找速度
1、首先用multiset存放words中的所有单词
2、遍历s，如果找到words中的某个单词，就在multiset中删除，直到multiset为空，如果没有找到则继续往后查找
3、返回下标的集合
```cpp
class Solution {
public:
    vector<int> findSubstring(string s, vector<string>& words) {
    	multiset<string> cnt;//用来存放words中的单词
    	for (int i = 0; i < words.size(); i++)
    	{
    		cnt.insert(words[i]);//初始化
    	}
    	vector<int> ret;
    	int lenw = words[0].length();
    	int total = words.size() * lenw;
    	int i, j;
    	if (s.length() < total) return ret;
    	for (i = 0; i <= s.length() - total;i++)
    	{
    		multiset<string> tempcnt = cnt;//拷贝一个副本
    		for (j = i; j < s.length(); j += lenw)
    		{
    			string temp = s.substr(j, lenw);
    			auto iter = tempcnt.find(temp);
    			if (iter != tempcnt.end())//找到了
    			{
    				tempcnt.erase(iter);//先删除该元素
    				if (tempcnt.empty()) {//为空代表找到了words中的所有单词按一定顺序排列的子串
    					ret.push_back(i);
    					break;
    				}
    			}
    			else {//没找到
    				break;
    			}
    		}
    	}
    	return ret;
    }
};
```