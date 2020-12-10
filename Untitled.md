### leetcode_38_easy_外观数列

![image-20201209190900752](Untitled.assets/image-20201209190900752.png)

![image-20201209190917768](Untitled.assets/image-20201209190917768.png)

```c++
class Solution {
public:
    string countAndSay(int n) {

    }
};
```

#### 算法思路

递推，知道当前字符串，即可求得下一个字符串。

递推求解过程，可以用**双指针**。左指针指向重复字符的左端点，右指针指向重复字符的右端点。注意避免指针越界。

```c++
class Solution {
public:
	string countAndSay(int n) {
		int i, left, right;
		string formerStr,curStr;
		vector<string> v;

		v.push_back("1");
		for (i = 1; i < n; i++)
		{
			formerStr = v[i - 1];
			curStr = "";
			left = right = 0;
			while (left < formerStr.size())
			{
				right = left;
				while (right < formerStr.size() - 1 && formerStr[left] == formerStr[right+1])
					right++;
				curStr.push_back(right - left + '1');  //该数字不会大于10 所以可以这样操作
				curStr.push_back(formerStr[left]);  //重复出现的数字
				left = right + 1;
			}
			v.push_back(curStr);
		}
		return v[n - 1];
	}
};
```

