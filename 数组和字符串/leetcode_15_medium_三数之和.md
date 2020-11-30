### leetcode_15_medium_三数之和

![image-20201128201212305](leetcode_15_medium_%E4%B8%89%E6%95%B0%E4%B9%8B%E5%92%8C.assets/image-20201128201212305.png)

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {

    }
};
```

#### 算法思路

暴力算法：枚举每一个三元组，判断是否和为0。时间复杂度O(n^3)，且需要去重操作。

以下在暴力法的基础上改进。

##### 三元组去重

例如，三个数为-3,1,2。则 三元组(-3,1,2)、(2,-3,1)、(1,2,-3)等表示的是同一个三元组，可以只保留一个升序版本(-3,1,2)。

因此，可以先**将nums排序**，那么 下标升序的三元组，其元素也是升序。时间复杂度O(n*logn)

##### 双指针

将三元组的三个下标记为a,b,c，其中a<b<c。

最外层循环为for(a=0;a<nums.size()-2;a++){}

对于给定的下标a，如何寻找对应的下标b,c，使得nums[a]+nums[b]+nums[c]==0?

首先假定内层循环为for(b=a+1;b<nums.size()-1;b++){}

对于已经找到的满足条件的三元组(a,b,c)，nums[a]+nums[b]+nums[c]==0。寻找下一个三元组(a,b',c')。由上述内层循环可得，**b'>b**，则nums[b']>=nums[b]。所以，满足条件的c'必有nums[c']<=nums[c]，也就是**c'<c**。也就是说，对于给定的a，可以将b，c设置为两个指针，从两侧向中间收缩。总的时间复杂度O(n^2)。

##### 双指针收缩的方法

讨论对于三元组(a,b,c)，如何寻找下一个用于测试的三元组

- 如果nums[a]+nums[b]+nums[c]==0，则找到了一个符合条件的三元组。下一组b、c，都不能用相同的。所以，b++，a--
- 如果nums[a]+nums[b]+nums[c]<0，则需要使三数之和更大。所以b++
- 如果nums[a]+nums[b]+nums[c]>0，则需要使三数之和更小，所以c--

##### 元素去重

当第一个指针迭代到a处时。如果nums[a-1]==nums[a]，那么，所有满足三数之和为0的三元组(a,b,c)，均有(a-1,b,c)也满足三数之和为0，而这样的三元组已经在上一次循环中被讨论过了，所以a处无需再讨论。可以跳过。

b，c同理。

当讨论a、b、c是否涉及元素重复时，注意比较时**数组下表越界检测**

```c++
class Solution {
public:
	vector<vector<int>> threeSum(vector<int>& nums) {
		int a, b, c;  //三个下标
		int sum;
		vector<vector<int>> results;

		if (nums.size() < 3)
			return results;
		sort(nums.begin(), nums.end());
		a = 0;
		while (a < nums.size() - 2)
		{
			b = a + 1;
			c = nums.size() - 1;
			while (b < c)
			{
				sum = nums[a] + nums[b] + nums[c];
				//根据本次的三数之和，调节双指针当中的一个
				if (sum == 0)
				{
					results.push_back(vector<int>{nums[a], nums[b], nums[c]});
					b++;
					c--;
				}
				else if (sum < 0)
					b++;
				else
					c--;

				//跳过重复元素
				while (b > a + 1 && b < c&&nums[b] == nums[b - 1])
					b++;
				while (c < nums.size() - 1 && b < c&& nums[c] == nums[c + 1])
					c--;
			}
			a++;
			while (a > 0 && a < nums.size() && nums[a] == nums[a - 1])  //跳过重复元素
				a++;
		}
		return results;
	}
};

```

