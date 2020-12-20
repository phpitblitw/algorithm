### leetcode_50_medium_Pow(x,n)

![image-20201218194630978](leetcode_50_medium_Pow(x,n).assets/image-20201218194630978.png)

```c++
class Solution {
public:
    double myPow(double x, int n) {

    }
};
```

#### 算法思路

O(n)的算法很简单，累乘n次即可。

可以优化到O(logn)。例如  求2^11，11记为2进制，即1011。所以结果为2^8 * 2^2 * 2^1。

注意代码中使用了**位运算**以减少运算量。

##### 边界情况

这题中，对于n=INT_MIN的特殊情况，并不能简单地取反。因此，需要单独讨论。多累乘一次1/x，然后取n=INT_MAX。因为abs(INT_MIN)=abs(INT_MAX)+1

```c++
class Solution {
public:
	double myPow(double x, int n) {
		double num;  //用来暂存x的幂
		double result;
		vector<double> multiplier;  //结果为其中的数的累乘

		if (n == 0)
			return 1;
		else if (n == INT_MIN)
		{
			x = 1 / x;
			n = INT_MAX;
			multiplier.push_back(x);
		}
		else if (n < 0)
		{
			x = 1 / x;
			n = -n;
		}

		//计算结果由哪些数累乘获得
		num = x;
		while (n > 0)
		{
			if (n & 1)  //如果n的末位是1
			{
				multiplier.push_back(num);
			}
			num *= num;
			n = n >> 1;
		}
		//累乘
		result = 1;
		for (int i = 0; i < multiplier.size(); i++)
		{
			result *= multiplier[i];
		}
		return result;
	}
};
```

