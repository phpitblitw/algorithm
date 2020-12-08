### leetcode_32_hard_最长有效括号

![image-20201208104359240](leetcode_32_hard_最长有效括号.assets/image-20201208104359240.png)

```
class Solution {
public:
    int longestValidParentheses(string s) {

    }
};
```

#### 算法思路

考虑使用动态规划算法，构造dp数组。

##### dp数组的规定

- 当s[n]为右括号时
  - 如果存在以s[n]为右端点的子串，dp[n]记录以s[n]为右端点的最长子串，左端点的位置。
  - 如果没有以s[n]为右端点的子串，dp[n]=-1
- 当s[n]为左括号时，dp[n]=-1

另外，根据题解https://leetcode-cn.com/problems/longest-valid-parentheses/solution/zui-chang-you-xiao-gua-hao-by-leetcode-solution/，也可以规定dp[n]为以下标n结尾的最长有效子串的长度。

##### dp算法的正确性

当s[n]是右括号时，最多存在一个左括号，与s[n]匹配。因为：

- 根据数学归纳法，规定，对于s[n]左侧的每一个右括号，都有0或1个左括号与之匹配
- 对于s[n]，向左找到的第一个未被匹配的左括号，与s[n]匹配

##### dp算法的实现

当求解dp[i]时，初始化一个指针j=i-1，用于寻找 以s[i]为右端点的最长子串 左端点的位置。首先  要找到与s[i]这个右括号匹配的左括号

- 如果当前j位置是个右括号 且有对应的子串，即dp[j]>=0，那么 左移指针 j=dp[j]-1，从而跳过这个子串
- 如果当前j位置是个右括号，且没有对应的子串，即dp[j]==-1&&s[j]=')'，那么 i 处的右括号也无法匹配到对应的子串
- 如果当前j位置是个左括号，则找到了与s[i]匹配的左括号。匹配成功！此外，仍然需要向左扩展，使得子串尽可能长。

```c++
class Solution {
public:
	int longestValidParentheses(string s) {
		int i, j, result;
		vector<int> dp(s.size(), -1);  //对于每一个右括号，记录以它为右端点的最长子串 左端点的位置；若为左括号或者没有子串 记-1

		//构造dp数组
		for (i = 0; i < s.size(); i++)
		{
			if (s[i] == ')')
			{
				j = i - 1;  //j指针 用来寻找与s[i]处的右括号相匹配的左括号
				while (j >= 0)  //向前寻找对应的左括号
				{
					if (dp[j] >= 0)  //当前j位置，是一个右括号，且有与之匹配的左括号
					{
						j = dp[j] - 1;  //左移指针 到下一个候选位置
					}
					else if (s[j] == ')')  //j处的右括号 尚且无法找到与之匹配的左括号。则i处的右括号也无法匹配
					{
						dp[i] = -1;  //匹配失败
						break;
					}
					else  //j处是一个尚未被匹配到的左括号
					{
						dp[i] = j;  //匹配成功（其实这行用不着）
						while (j > 0 && dp[j - 1] >= 0)  //向左扩展
						{
							j = dp[j - 1];
						}
						dp[i] = j;
						break;
					}
				}
				if (j < 0)
					dp[i] = -1;  //找到左侧尽头都没找到匹配的左指针
			}
		}
		//找到最长子串
		result = 0;
		for (i = 0; i < s.size(); i++)
			if(dp[i]>=0)
				result = max(result, i - dp[i] + 1);

		return result;
	}
};
```

