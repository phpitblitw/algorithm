### leetcode_221_medium_最大正方形

![image-20210301201804266](leetcode_221_medium_%E6%9C%80%E5%A4%A7%E6%AD%A3%E6%96%B9%E5%BD%A2.assets/image-20210301201804266.png)

```c++
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {

    }
};
```

#### 算法思路

dp算法。令maxLength[y] [x]表示以(y,x)为右下角点的正方形的最大边长。则考虑该正方形由左侧正方形+上方正方形组合而来

```c++
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        int y, x, length;
        int height = matrix.size(), width = matrix[0].size(), result = 0;
        vector<vector<int>> maxLength(height, vector<int>(width, 0));

        for (y = 0; y < height; y++)
        {
            for (x = 0; x < width; x++)
            {
                if (matrix[y][x] == '0')  //无法组成正方形
                    maxLength[y][x] = 0;
                else if (y == 0 || x == 0)  //边界
                {
                    maxLength[y][x] = 1;
                    result = max(result, 1);
                }
                else
                {
                    length = min(maxLength[y - 1][x], maxLength[y][x - 1]);
                    if (matrix[y - length][x - length] == '1')  //两个小正方形可以组合成一个大正方形
                        maxLength[y][x] = length + 1;
                    else  //两个小正方形无法组合成一个大正方形
                        maxLength[y][x] = length;
                    result = max(result, maxLength[y][x]);
                }
            }
        }
        return result * result;
    }
};
```

