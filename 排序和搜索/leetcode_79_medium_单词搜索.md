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

```c++
class Solution {
public:
	bool exist(vector<vector<char>>& board, string word) {
		int y, x, height, width;
		vector<vector<bool>> used;

		if (board.empty() || board[0].empty())
			return false;
		height = board.size();
		width = board[0].size();
		used = vector<vector<bool>>(height, vector<bool>(width, false));
		for (y = 0; y < height; y++)
		{
			for (x = 0; x < width; x++)
			{
				if (backtrack(y, x, 0, word, board, used))
					return true;
			}
		}
		return false;
	}

	//判断[y,x]处是否为word[index]字符，并继续搜索
	bool backtrack(int y, int x, int index, string & word, vector<vector<char>>& board, vector<vector<bool>>& used)
	{
		if (index == word.size())  //搜索完成
			return true;
		if (y < 0 || y >= used.size() || x < 0 || x >= used[0].size())  //越界 则该路径搜索失败
			return false;
		if (used[y][x])  //重复搜索检测
			return false;
		if (board[y][x] != word[index])  //字符一致检测
			return false;

		used[y][x] = true;
		if (backtrack(y - 1, x, index + 1, word, board, used)
			|| backtrack(y + 1, x, index + 1, word, board, used)
			|| backtrack(y, x - 1, index + 1, word, board, used)
			|| backtrack(y, x + 1, index + 1, word, board, used))
			return true;
		else
		{
			used[y][x] = false;
			return false;
		}
	}
};
```

