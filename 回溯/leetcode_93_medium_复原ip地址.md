### leetcode_93_medium_复原ip地址

![image-20210110163121339](leetcode_93_medium_%E5%A4%8D%E5%8E%9Fip%E5%9C%B0%E5%9D%80.assets/image-20210110163121339.png)

![image-20210110163142787](leetcode_93_medium_%E5%A4%8D%E5%8E%9Fip%E5%9C%B0%E5%9D%80.assets/image-20210110163142787.png)

![image-20210110163154896](leetcode_93_medium_%E5%A4%8D%E5%8E%9Fip%E5%9C%B0%E5%9D%80.assets/image-20210110163154896.png)

```c++
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {

    }
};
```

#### 算法思路

回溯算法。用1~3个字符，形成ip地址的当前字段，来作为3个不同的分支

```c++
class Solution {
public:
	vector<string> restoreIpAddresses(string s) {
		string curStr;
		vector<string> results;
		backtrack(0, 0, curStr, s, results);
		return results;
	}

	//正在处理第fieldIndex个字段(0<=fieldIndex<=3),可以使用从第charIndex个开始的字符,处理ip地址字符串 ip
	void backtrack(int fieldIndex, int charIndex, string &curStr,string &ip, vector<string> &results)
	{
		int i;
		string numStr;  //表示ip地址当前字段的字符串
		//构造ip地址成功的情况
		if (fieldIndex == 4 && charIndex == ip.size())
		{
			results.push_back(curStr);
			return;
		}
		//剩余的字符数一定无法用于构造ip地址
		if ((4 - fieldIndex) * 1 > ip.size() - charIndex
			|| (4 - fieldIndex) * 3 < ip.size() - charIndex)
			return;
		//添加ip地址字段之间的分隔符
		if (fieldIndex > 0)
			curStr += '.';
		//构造ip地址的当前字段
		for (i = 1; i <= min(3,int(ip.size())-charIndex); i++)
		{
			numStr = ip.substr(charIndex, i);  //尝试用这个字符串，作为ip地址的当前字段
			if (stoi(numStr) < 0 || stoi(numStr) > 255)  //字段越界
				continue;
			if (numStr[0] == '0' && i > 1)  //含有前导0
				continue;
			curStr += numStr;
			backtrack(fieldIndex + 1, charIndex + i, curStr, ip, results);
			curStr = curStr.substr(0,curStr.size() - i);
		}
		curStr = curStr.substr(0,curStr.size() - 1);  //移除'.'
	}
};
```

