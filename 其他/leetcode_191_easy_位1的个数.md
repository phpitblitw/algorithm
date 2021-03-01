### leetcode_191_easy_位1的个数

![image-20210217115338464](leetcode_191_easy_位1的个数.assets/image-20210217115338464.png)

![image-20210217115351163](leetcode_191_easy_位1的个数.assets/image-20210217115351163.png)

![image-20210217115401805](leetcode_191_easy_位1的个数.assets/image-20210217115401805.png)

```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        
    }
};
```

#### 算法思路

按位计算1的数量。考察位运算

```c++
class Solution {
public:
	int hammingWeight(uint32_t n) {
		int result = 0;
		while (n > 0)
		{
			if (n & 1)
				++result;
			n = n >> 1;
		}
		return result;
	}
};

```

