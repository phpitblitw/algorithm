### leetcode_209_medium_长度最小的子数组

![image-20210224112026251](leetcode_209_medium_长度最小的子数组.assets/image-20210224112026251.png)

![image-20210224112036850](leetcode_209_medium_长度最小的子数组.assets/image-20210224112036850.png)

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {

    }
};
```

#### 滑动窗口法

```c++
class Solution {
public:
	int minSubArrayLen(int target, vector<int>& nums) {
		int l, r, sum, result = INT_MAX;  //[l,r]区间为当前子串

		for (l = 0, r = 0, sum = 0; r < nums.size(); r++)
		{
			sum += nums[r];
			while (l <= r && sum >= target)
			{
				result = min(result, r - l + 1);
				sum -= nums[l++];
			}
		}
		return result == INT_MAX ? 0 : result;
	}
};
```

#### 前缀和+二分查找

详见leetcode官方题解

![image-20210224113229012](leetcode_209_medium_长度最小的子数组.assets/image-20210224113229012.png)