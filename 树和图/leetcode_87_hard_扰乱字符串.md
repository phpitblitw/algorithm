### leetcode_87_hard_扰乱字符串

![image-20210106055624029](leetcode_87_hard_%E6%89%B0%E4%B9%B1%E5%AD%97%E7%AC%A6%E4%B8%B2.assets/image-20210106055624029.png)

![image-20210106055649193](leetcode_87_hard_%E6%89%B0%E4%B9%B1%E5%AD%97%E7%AC%A6%E4%B8%B2.assets/image-20210106055649193.png)

![image-20210106055717068](leetcode_87_hard_%E6%89%B0%E4%B9%B1%E5%AD%97%E7%AC%A6%E4%B8%B2.assets/image-20210106055717068.png)

```c++
class Solution {
public:
    bool isScramble(string s1, string s2) {

    }
};
```

#### 算法思路

##### 扰乱字符串的判别

关键是如何判断字符串s是扰乱字符串

讨论字符串s2，是否是字符串s1的扰乱字符串。

- 如果s1的前n个字符(n<s1.size()-1)，与s2的前n个字符对应；则可以继续讨论。
  例如，判断s1="great"，s2="rgtae"，前2个字符。"gr"与"rg"对应，则找到了二叉树的分割处。接下来 只需判断"gr"与"rg"是否为扰乱字符串即可。
- 如果s1的前n个字符(n<s1.size())，与s2的后n个字符对应；
- 如果无法找到一个n(n<si.size())，使得s1的前n个字符，匹配s2的前n/后n个字符，则s1 s2必不是扰乱字符串
  例如s1="abcde"，s2="caebd"，只能使得s1的前5个字符，匹配s2的前5个字符。即无法拆分二叉树。所以不是扰乱字符串

总的来说，判断是否是扰乱字符串，分为两步

1. 找到能否将s1的前n个字符，与s2的前n个 或 后n个字符匹配
2. 按照1所找到的分割，将s1与s2的两个对应子串，判断是否为扰乱字符串

##### 子串匹配的判别

以一种情况为例，讨论s1的前i个字符构成的子串，是否与s2的前j个字符构成的子串匹配

维护int diff[128]，记录对于ascll码的每一个字符，在s1的子串中，相比于在s2的子串中，多出现了多少次。这个数组用于辅助计算diffNum

维护 int diffNum，记录s1的子串与s2的子串，有多少种字符不同。

当i,j指向新的元素时，都会随之更新diff[]数组。当diff[c]由0变为其他值时，diffNum++。当diff[c]由其他值变为0时，diffNum--。

```c++
class Solution {
public:
	bool isScramble(string s1, string s2) {
		int i, j;
		int diffNum;  //s1的子串与s2的子串 有多少种字符出现的数量不同
		int diff[128];  //各个字符，在s1的子串中比在s2的子串中多出现了几次
		if (s1.size() != s2.size())
			return false;
		if (s1 == s2)
			return true;
		//试着将s1的前n个字符 与s2的前n个字符匹配
		diffNum = 0;
		memset(diff, 0, sizeof(int) * 128);
		for (i = 0, j = 0; i < s1.size()-1; i++, j++)
		{
			diff[s1[i]]++;
			if (diff[s1[i]] == 1) diffNum++;  //在s1[i]这个字符 出现了数量不同
			if (diff[s1[i]] == 0)diffNum--;  //在s1[i]这个字符，数量变为相同了
			diff[s2[j]]--;
			if (diff[s2[j]] == -1)  diffNum++;  //在s2[j]这个字符，出现了数量不同
			if (diff[s2[j]] == 0) diffNum--;  //在s2[j]这个字符，数量变为相同了
			if (diffNum == 0)
				if (isScramble(s1.substr(0, i+1), s2.substr(0, j+1))
					&& isScramble(s1.substr(i + 1), s2.substr(j + 1)))
					return true;
		}
		//试着将s1的前n个字符 与s2的后n个字符匹配
		diffNum = 0;
		memset(diff, 0, sizeof(int) * 128);
		for (i = 0, j = s2.size()-1; i < s1.size() - 1; i++, j--)
		{
			diff[s1[i]]++;
			if (diff[s1[i]] == 1) diffNum++;  //在s1[i]这个字符 出现了数量不同
			if (diff[s1[i]] == 0)diffNum--;  //在s1[i]这个字符，数量变为相同了
			diff[s2[j]]--;
			if (diff[s2[j]] == -1)  diffNum++;  //在s2[j]这个字符，出现了数量不同
			if (diff[s2[j]] == 0) diffNum--;  //在s2[j]这个字符，数量变为相同了
			if (diffNum == 0)
				if (isScramble(s1.substr(0, i + 1), s2.substr(j))
					&& isScramble(s1.substr(i + 1), s2.substr(0,j)))
					return true;
		}
		return false;
	}
};
```

另外，头文件<string> 中 函数 int memcmp (const void *s1, const void *s2, size_t n); 比较s1 s2所指向的内存区间的前n个字符 是否相同。相同取0，s1小返回-1，s1大返回1