### leetcode_97_hard_交错字符串

![image-20210111171806751](leetcode_97_hard_%E4%BA%A4%E9%94%99%E5%AD%97%E7%AC%A6%E4%B8%B2.assets/image-20210111171806751.png)

![image-20210111171829220](leetcode_97_hard_%E4%BA%A4%E9%94%99%E5%AD%97%E7%AC%A6%E4%B8%B2.assets/image-20210111171829220.png)

![image-20210111171844987](leetcode_97_hard_%E4%BA%A4%E9%94%99%E5%AD%97%E7%AC%A6%E4%B8%B2.assets/image-20210111171844987.png)

#### 算法思路

构造二维动态规划数组match[] []。其中，match[m] [n] 表示，s1的前m个字母(下标从1开始)，与s2的前n个字母，交错后能否得到s3的前m+n个字母。

```c++
class Solution {
public:
	bool isInterleave(string s1, string s2, string s3) {
		int i, j;
		vector<vector<bool>> match(s1.size() + 1, vector<bool>(s2.size() + 1, false));  //s1的前m个字符(下标从1开始),与s2的前n个字符，是否能够组合成s3的前m+n个字符

		//一定不符合的情况
		if (s1.size() + s2.size() != s3.size())
			return false;

		match[0][0] = true;
		//首列
		for (i = 1; i <= s1.size(); i++)
			match[i][0] = match[i - 1][0] && s1[i-1] == s3[i-1];
		//首行
		for (j = 1; j <= s2.size(); j++)
			match[0][j] = match[0][j - 1] && s2[j-1] == s3[j-1];
		//其他位置
		for (i = 1; i <= s1.size(); i++)
		{
			for (j = 1; j <= s2.size(); j++)
			{
				if (match[i][j - 1] && s2[j - 1] == s3[i + j - 1])
					match[i][j] = true;
				else if (match[i - 1][j] && s1[i - 1] == s3[i + j - 1])
					match[i][j] = true;
				else
					match[i][j] = false;
			}
		}
		return match[s1.size()][s2.size()];
	}
};
```

