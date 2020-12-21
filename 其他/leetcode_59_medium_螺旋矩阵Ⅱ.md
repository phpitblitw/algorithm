### leetcode_59_medium_螺旋矩阵Ⅱ

![image-20201221160232841](leetcode_59_medium_%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5%E2%85%A1.assets/image-20201221160232841.png)

```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {

    }
};
```

#### 算法思路

类似leetcode_54_medium_螺旋矩阵。指针按照 右->下->左->上 的顺序移动，直到访问完所有位置为止

```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        int i, num, y, x,newY,newX,dir;
        static int dx[4]{ 1,0,-1,0 };
        static int dy[4]{ 0,1,0,-1 };
        vector<vector<int>> result(n, vector<int>(n, 0));  //矩阵初值置为0 代表尚未赋值

        num = n * n;
        y = x = 0;
        dir = 0;  //初始方向为向右
        for (i = 1; i <= num; i++)
        {
            //为当前位置赋值
            result[y][x] = i;
            //判断是否需要改变方向
            newY = y + dy[dir];
            newX = x + dx[dir];
            if (newX < 0 || newX >= n || newY < 0 || newY >= n || result[newY][newX] != 0)
                dir = (dir + 1) % 4;
            //确定下一个待访问的位置
            y += dy[dir];
            x += dx[dir];
        }
        return result;
    }
};
```

