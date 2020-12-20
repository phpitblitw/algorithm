### leetcode_55_medium_跳跃游戏

![image-20201220205711303](leetcode_55_medium_%E8%B7%B3%E8%B7%83%E6%B8%B8%E6%88%8F.assets/image-20201220205711303.png)

```c++
class Solution {
public:
    bool canJump(vector<int>& nums) {

    }
};
```

#### 算法思路

维护一个变量range，记录当前讨论过的所有节点，所能到达的最远位置。

对于讨论的每一个节点nums[i]=k，那么[i+1,i+k]这些区间内的所有元素，都是可以被访问到的。那么，用最远的位置更新range

```c++
class Solution {
public:
	bool canJump(vector<int>& nums) {
		int range,i;

		if (nums.empty())
			return true;
		range = 0;
		for (i = 0; i < nums.size(); i++)
		{
			if (range < i)
				return false;
			range = max(range, nums[i]+i);
		}
		return true;
	}
};
```

