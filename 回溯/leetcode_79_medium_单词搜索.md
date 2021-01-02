### leetcode_79_medium_单词搜索

![image-20201230101938103](leetcode_79_medium_单词搜索.assets/image-20201230101938103.png)

```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {

    }
};
```

#### 算法思路

每找到一个单词的起始点，从这个位置开始dfs搜索。搜索失败则回溯