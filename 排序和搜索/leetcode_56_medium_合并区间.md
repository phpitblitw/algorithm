

### leetcode_56_medium_合并区间

![image-20201221142928795](leetcode_56_medium_%E5%90%88%E5%B9%B6%E5%8C%BA%E9%97%B4.assets/image-20201221142928795.png)

```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {

    }
};
```

#### 算法思路

1. 将所有的区间，按照左端点的大小排序
2. 每当讨论第i个区间时，尝试与后面的区间合并。

关于步骤2的正确性：

- 讨论到第i个区间时，前i-1个区间已经合并完成。故前i-1个区间与第i个及以后的区间不重合
- 第i个区间，如果与至少一个其他区间重合的话，那么一定是intervals[i] [1]在其他区间的范围内。那么必与第i+1个区间重合。
- 那么，融合第i，i+1个区间，再继续讨论

```c++
class Solution {
public:
    static bool cmp(const vector<int>& a, const vector<int>& b)
    {
        return a[0] < b[0];
    }

    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        int i,curLeft, curRight,size=intervals.size();
        vector<vector<int>> result;

        sort(intervals.begin(), intervals.end(),cmp);
        for (i = 0; i < size; i++)
        {
            curLeft = intervals[i][0];
            curRight = intervals[i][1];
            while (i < size - 1 && intervals[i + 1][0] <= curRight)  //如果和下一个区间有重合
            {
                i++;  //开始讨论下一个区间
                curRight = max(curRight, intervals[i][1]);  //合并区间
            }
            result.push_back(vector<int>{curLeft, curRight});
        }
        return result;

    }
};
```

