### leetcode_28_easy_实现strStr()

![image-20201204113858229](leetcode_28_easy_实现strStr().assets/image-20201204113858229.png)

```c++
class Solution {
public:
    int strStr(string haystack, string needle) {

    }
};
```

#### 算法思路

建立函数isEqual()，比较haystack从index开始的元素，是否与needle匹配。

注意，string::size()的返回值为unsigned_int64类型的。两个size()相减，可能会发生越界。因此，**size()之间的减法操作，需要强转为int进行**。

![image-20201204123319080](leetcode_28_easy_实现strStr().assets/image-20201204123319080.png)

![image-20201204123335845](leetcode_28_easy_实现strStr().assets/image-20201204123335845.png)

```c++
class Solution {
public:
	int strStr(string haystack, string needle) {
		int length = needle.length();
		int i;
		if (needle.empty())
			return 0;
		for (i = 0; i <= int(haystack.length()) - length; i++)  //注意此处强制类型转换
		{
			if (isEqual(haystack, needle, i))
				return i;
		}
		return -1;
	}
	bool isEqual(string& haystack, string& needle, int index)  //判断haystack从index开始的子串，是否与needle相同
	{
		for (int i = 0; i < needle.size(); i++)
		{
			if (haystack[index+i] != needle[i])
				return false;
		}
		return true;
	}
};
```

