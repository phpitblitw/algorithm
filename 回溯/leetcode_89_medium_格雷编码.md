### leetcode_89_medium_格雷编码

![image-20210109144031752](leetcode_89_medium_%E6%A0%BC%E9%9B%B7%E7%BC%96%E7%A0%81.assets/image-20210109144031752.png)

![image-20210109144049161](leetcode_89_medium_%E6%A0%BC%E9%9B%B7%E7%BC%96%E7%A0%81.assets/image-20210109144049161.png)

![image-20210109144110759](leetcode_89_medium_%E6%A0%BC%E9%9B%B7%E7%BC%96%E7%A0%81.assets/image-20210109144110759.png)

```c++
class Solution {
public:
    vector<int> grayCode(int n) {

    }
};
```

#### 回溯法

回溯法。对于给定的n，要求一个长度为2^n的格雷编码序列。

已经找到前i-1个元素，求第i个元素时，可以通过回溯算法。先分别尝试修改res[i-1]的各个bit位，能否继续回溯过程

```c++
class Solution {
public:
	vector<int> grayCode(int n) {
		vector<int> res;
		unordered_set<int> used;

		if (n <= 0)
			return vector<int>();
		res.push_back(0);
		used.insert(0);
		backtrack(n, res, used);
		return res;
	}

	bool backtrack(int n,vector<int>& res, unordered_set<int>& used)
	{
		int i, last, next;
		if (res.size() == 1 << n)
			return true;
		last = res.back();
		for (i = 0; i < n; i++)  //尝试改变last的各个bit位
		{
			next = last ^ (1 << i);  //修改从低位开始 第i个bit
			if (used.count(next))  //检测这个编码是否被使用过
				continue;
			res.push_back(next);
			used.insert(next);
			if (backtrack(n, res, used))  //格雷码编码成功
				return true;
			else
			{
				res.pop_back();
				used.erase(next);
			}
		}
		return false;  //没有符合要求的格雷码编码
	}
};
```

![image-20210109145654800](leetcode_89_medium_%E6%A0%BC%E9%9B%B7%E7%BC%96%E7%A0%81.assets/image-20210109145654800.png)