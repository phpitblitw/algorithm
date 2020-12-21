### leetcode_58_easy_最后一个单词的长度

![image-20201221155949617](leetcode_58_easy_%E6%9C%80%E5%90%8E%E4%B8%80%E4%B8%AA%E5%8D%95%E8%AF%8D%E7%9A%84%E9%95%BF%E5%BA%A6.assets/image-20201221155949617.png)

```c++
class Solution {
public:
    int lengthOfLastWord(string s) {

    }
};
```

#### 算法思路

从后向前查找

1. 跳过每一个空格
2. 为每一个字母计数

```c++
class Solution {
public:
    int lengthOfLastWord(string s) {
        int i, result = 0;
        //跳过空格
        i = s.size() - 1;
        while (i >= 0 && s[i] == ' ')
            i--;
        //查找单词长度
        while (i >= 0 && s[i] != ' ')
        {
            result++;
            i--;
        }
        return result;
    }
};
```

