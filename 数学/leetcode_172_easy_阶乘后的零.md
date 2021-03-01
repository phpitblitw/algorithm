### leetcode_172_easy_阶乘后的零

![image-20210216112306087](leetcode_172_easy_阶乘后的零.assets/image-20210216112306087.png)

```c++
class Solution {
public:
    int trailingZeroes(int n) {

    }
};
```

#### 算法思路

阶乘结果中的0，均是由2*5这样的因子得出。易证，在n!的诸多乘数中，因子5出现的次数多于因子2出现的次数，所以，统计因子5出现的次数即可。

参考https://leetcode-cn.com/problems/factorial-trailing-zeroes/solution/xiang-xi-tong-su-de-si-lu-fen-xi-by-windliang-3/

```c++
class Solution {
public:
	int trailingZeroes(int n) {
		int result = 0;
		while (n > 0)
		{
			result += n / 5; 
			n /= 5;
		}
        return result;
	}
};
```

