### leetcode_88_easy_合并两个有序数组

![image-20210109132001199](leetcode_88_easy_%E5%90%88%E5%B9%B6%E4%B8%A4%E4%B8%AA%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84.assets/image-20210109132001199.png)

![image-20210109132116337](leetcode_88_easy_%E5%90%88%E5%B9%B6%E4%B8%A4%E4%B8%AA%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84.assets/image-20210109132116337.png)

```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {

    }
};
```

#### 算法思路

将数组nums2合并到数组nums1中。

为了避免nums2中的元素覆盖了nums1中的元素，所以，从后向前合并。依次将nums1,nums2中较大的元素，放置到结果数组中

```c++
class Solution {
public:
	void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
		int i, j, k;
		i = m - 1;  //访问nums1的指针
		j = n - 1;  //访问nums2的指针
		k = m + n - 1;  //指向即将存放结果数据的指针
		//从后向前访问，将较大的元素先放入结果数组
		while (i >= 0 && j >= 0)
		{
			if (nums1[i] >= nums2[j])
				nums1[k--] = nums1[i--];
			else
				nums1[k--] = nums2[j--];
		}
		//如果nums1还有剩余，则无需操作
		//如果nums2还有剩余，则复制到结果数组中
		while (j >= 0)
			nums1[k--] = nums2[j--];
	}
};
```

