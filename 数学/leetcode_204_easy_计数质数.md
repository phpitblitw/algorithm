### leetcode_204_easy_计数质数.md

![image-20210218191601100](leetcode_204_计数质数.assets/image-20210218191601100.png)

![image-20210218191611041](leetcode_204_计数质数.assets/image-20210218191611041.png)

```c++
class Solution {
public:
    int countPrimes(int n) {

    }
};
```

#### 枚举法1

判断k是否为质数，即判断能否被[2,√k]整除。

```c++
class Solution {
public:
	int countPrimes(int n) {
		int i,result = 0;

		for (i = 2; i < n; i++)
		{
			if (isPrime(i))
				result++;
		}
		return result;
	}

	bool isPrime(int n)
	{
		int i;
		
		for (i = 2; i*i <= n; i++)
		{
			if (n%i == 0)
				return false;
		}
		return true;
	}
};
```

![image-20210218202856504](leetcode_204_计数质数.assets/image-20210218202856504.png)

#### 枚举法2

与上面的唯一区别在于，使用了sqrt()

```c++
class Solution {
public:
	int countPrimes(int n) {
		int i,result = 0;

		for (i = 2; i < n; i++)
		{
			if (isPrime(i))
				result++;
		}
		return result;
	}

	bool isPrime(int n)
	{
		int i;
		
		for (i = 2; i <= sqrt(n); i++)
		{
			if (n%i == 0)
				return false;
		}
		return true;
	}
};
```

![image-20210218195840442](leetcode_204_计数质数.assets/image-20210218195840442.png)

#### 埃氏筛

![image-20210218200023545](leetcode_204_计数质数.assets/image-20210218200023545.png)

```c++
class Solution {
public:
	int countPrimes(int n) {
		int i, j, result = 0;
		vector<bool> isPrime(n, true);  //数字k是否为质数

		for (i = 2; i < n; i++)
		{
			if (isPrime[i])
				result++;
			if ((long long)i*i > n)
				continue;
			for (j = i * i; j < n; j += i)  //将i的所有倍数记为合数
			{
				isPrime[j] = false;
			}
		}
		return result;
	}
};
```

![image-20210218202835546](leetcode_204_计数质数.assets/image-20210218202835546.png)