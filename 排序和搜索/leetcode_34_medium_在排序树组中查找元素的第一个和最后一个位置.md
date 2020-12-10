### leetcode_34_medium_在排序树组中查找元素的第一个和最后一个位置

![image-20201208200053350](leetcode_34_medium_在排序树组中查找元素的第一个和最后一个位置.assets/image-20201208200053350.png)

```c++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {

    }
};
```

#### 算法思路

首先，二分查找，找到一个值为target的位置。

之后，分别向左 向右 扩展指针

```c++
class Solution {
public:
	vector<int> searchRange(vector<int>& nums, int target) {
		int left, right, mid;

		if (nums.empty())
			return vector<int> {-1, -1};
		left = 0;
		right = nums.size() - 1;
		//二分查找一个等于target的位置
		while (left <= right)
		{
			mid = (left + right) / 2;
			if (nums[mid] == target)
				break;
			else if (target<nums[mid])
				right = mid - 1;
			else
				left = mid + 1;
		}
		if (nums[mid] != target)  //没找到的情况
			return vector<int>{-1, -1};
		//分别向左右扩展
		left = mid;
		while (left > 0 && nums[left-1] == target)
			left--;
		right = mid;
		while (right < nums.size() - 1 && nums[right + 1] == target)
			right++;
		return vector<int>{left, right};
	}
};
```

