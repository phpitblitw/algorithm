### leetcode_90_medium_子集

![image-20210109191010734](leetcode_90_medium_%E5%AD%90%E9%9B%86.assets/image-20210109191010734.png)

```c++
class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        
    }
};
```

#### 算法思路

回溯法。首先需要将所有元素排序。

关于解集不能包含重复的子集。例如，nums=[1,2,2]的情况，为了方便讨论，将两个数字2区分为2_1、2_2。则子集[1,2_1]和子集[1,2_2]其实是重复的子集。

也就是，对于重复出现的元素，需要找到一种方法避免其产生相同的子集。

通过下述方法。例如上述例子，如果2_1没有在子集中出现的话，就不能将2_2加入子集。从而避免重复。

```c++
class Solution {
public:
	vector<vector<int>> subsetsWithDup(vector<int>& nums) {
		sort(nums.begin(), nums.end());
		vector<int> subset;
		vector<vector<int>> results;
		backtrack(0, subset, nums, results);
		return results;
	}

	void backtrack(int i, vector<int>& subset, vector<int>& nums,vector<vector<int>>& results)
	{
		if (i == nums.size())
		{
			results.push_back(subset);
			return;
		}
		//添加第i个元素的分支
		subset.push_back(nums[i]);
		backtrack(i + 1, subset, nums, results);
		subset.pop_back();
		//不添加第i个元素的分支
		while (i < nums.size() - 1 && nums[i] == nums[i + 1])  //如果决定不要nums[i]这个元素，则所有与nums[i]相同的元素都不要
			i++;
		backtrack(i + 1, subset, nums, results);
	}
};
```

