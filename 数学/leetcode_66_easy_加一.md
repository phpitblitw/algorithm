### leetcode_66_easy_加一

![image-20201222202446891](leetcode_66_easy_加一.assets/image-20201222202446891.png)

```c++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {

    }
};
```

#### 算法思路

注意digits每一位数字全为9的特殊情况即可

```c++
class Solution {
public:
	vector<int> plusOne(vector<int>& digits) {
		int i;
		vector<int> result(digits);
		for (i = digits.size()-1; i >= 0; i--)
		{
			if (digits[i] < 9)
			{
				result[i]++;
				break;
			}	
			else
				result[i] = 0;
		}
		if (i == -1)  //这意味着原来的digits全为9
		{
			result = vector<int>(digits.size() + 1, 0);
			result[0] = 1;
		}
		return result;
	}
};
```

