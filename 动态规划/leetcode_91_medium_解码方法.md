### leetcode_91_medium_解码方法

![image-20210109200648467](leetcode_91_medium_%E8%A7%A3%E7%A0%81%E6%96%B9%E6%B3%95.assets/image-20210109200648467.png)

![image-20210109200709143](leetcode_91_medium_%E8%A7%A3%E7%A0%81%E6%96%B9%E6%B3%95.assets/image-20210109200709143.png)

![image-20210109200725100](leetcode_91_medium_%E8%A7%A3%E7%A0%81%E6%96%B9%E6%B3%95.assets/image-20210109200725100.png)

```c++
class Solution {
public:
    int numDecodings(string s) {

    }
};
```

#### 算法思路

动态规划。构造数组dp。dp[i]表示 s的前i个字符，有多少种解码的方法。

关键在于状态转移方程。dp初始值均为0。讨论dp[i]

- 如果s[i-1] s[i]两个字符，能够编码一个字母。这隐含两个条件。i>0，以及s[i-1] s[i]对应的数 在1~26范围内
  - 如果i>1，则是在dp[i-2]的基础上，将s[i-1] s[i]编码成一个字母。dp[i]+=dp[i-2]
  - 如果i=1，则是直接将s的前2个字符，编码成一个字母。dp[i]+=1
- 如果s[i]能够编码成一个字母。即s[i]在(0,9]区间内
  - 如果i>0，则是在dp[i-1]的基础上，将s[i]编码成一个字母。dp[i]+=dp[i-1]
  - 如果i=0，则是直接将s的第1个字符，编码成一个字母。dp[i]+=1

```c++
class Solution {
public:
	int numDecodings(string s) {
		int i, num;
		vector<int> dp(s.size(), 0);  //s的前i个字符，有多少种解码的方法
		
		for (i = 0; i < dp.size(); i++)
		{
			if (i > 0)  //包括当前字符 至少有2个字符
			{
				num = (s[i - 1] - '0') * 10 + s[i] - '0';
				if (10 <= num && num <= 26)  //如果当前以及前一个字符 可以编码一个字母
				{
					if (i > 1)
						dp[i] += dp[i - 2];
					else
						dp[i]++;
				}
			}
			if ('0' < s[i] && s[i] <= '9')  //如果当前字符 可以编码一个字母
			{
				if (i > 0)
					dp[i] += dp[i - 1];
				else
					dp[i]++;
			}
		}
		return dp[dp.size() - 1];

	}
};
```

