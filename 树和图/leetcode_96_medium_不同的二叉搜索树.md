### leetcode_96_medium_不同的二叉搜索树

![image-20210111164833512](leetcode_96_medium_%E4%B8%8D%E5%90%8C%E7%9A%84%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210111164833512.png)

```c++
class Solution {
public:
    int numTrees(int n) {

    }
};
```

#### 递归算法

递归算法。与leetcode_95_medium_不同的二叉搜索树Ⅱ相同。超时

```c++
class Solution {
public:
	int numTrees(int n) {
		if (n <= 0)
			return 0;
		else
			return numTrees(1, n);
	}

	//[begin,end]区间共能够构造多少种二叉搜索树
	int numTrees(int begin, int end)
	{
		int mid, leftNum, rightNum, result;
		if (begin > end)
			return 1;
		for (mid = begin, result = 0; mid <= end; mid++)
		{
			leftNum = numTrees(begin, mid - 1);
			rightNum = numTrees(mid + 1, end);
			result += leftNum * rightNum;
		}
		return result;
	}
};
```

![image-20210111165536641](leetcode_96_medium_%E4%B8%8D%E5%90%8C%E7%9A%84%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210111165536641.png)

#### 动态规划

构造数组dp。dp[n]表示以1...n为节点组成的二叉搜索树有多少种

状态转移方程见代码，此处不赘述

```c++
class Solution {
public:
	int numTrees(int n) {
		int i,j, leftNum, rightNum;
		vector<int> dp(n + 1, 0);  //使用n个元素，可以形成多少种二叉搜索树

		//按照题意，n=0对应的二叉搜索树种类数为0
		if (n == 0)
			return 0;
		//其他情况
		dp[0] = 1;  //认为0个元素 能且只能形成1种二叉搜索树
		for (i = 1; i <= n; i++)  //讨论使用i个元素，可以形成多少种二叉搜索树
		{
			for (j = 1; j <= i; j++)  //以第j个元素作为根节点，将[1,i]这些节点分为两个子树
			{
				leftNum = dp[j - 1];  //左子树有多少种可能性
				rightNum = dp[i - j];  //右子树有多少种可能性
				dp[i] += leftNum * rightNum;
			}
		}
		return dp[n];
	}
};
```

