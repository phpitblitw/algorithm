### leetcode_67_easy_二进制求和

![image-20201223104833462](leetcode_67_easy_二进制求和.assets/image-20201223104833462.png)

```c++
class Solution {
public:
    string addBinary(string a, string b) {

    }
};
```

#### 算法思路

从低位到高位，按位相加即可。用carry存储进位

为了方便计算，可以使用**reverse()**函数。reverse(a.begin(),a.end())，翻转容器

```c
class Solution {
public:
	string addBinary(string a, string b) {
		int i, j, k, carry;
		int sizeA = a.size(), sizeB = b.size();
		string result;

		reverse(a.begin(), a.end());
		reverse(b.begin(), b.end());
		carry = 0;
		for (i = 0; i < max(sizeA, sizeB); i++)
		{
			carry += i < sizeA ? a[i] - '0' : 0;
			carry += i < sizeB ? b[i] - '0' : 0;
			result += (carry % 2) + '0';
			carry = carry >= 2 ? 1 : 0;
		}
		if (carry == 1)
			result += '1';
		reverse(result.begin(), result.end());
		return result;
	}
};
```

