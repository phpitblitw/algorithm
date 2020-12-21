### leetcode_57_hard_插入区间

![image-20201221143219673](leetcode_57_hard_%E6%8F%92%E5%85%A5%E5%8C%BA%E9%97%B4.assets/image-20201221143219673.png)

```c++
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {

    }
};
```

### 算法思路

原来的列表是有序且不重叠的。要保证新插入区间后，列表仍然有序且不重叠，那么，只要处理与新插入区间重合的区间即可。

原来序列中的所有区间，只有三种情况

- 与新区间完全不重合，且在新区间的左边。这些原区间保留即可
- 与新区间重合。这些区间，与新区间融合为一个区间
- 与新区间完全不重合，且在新区间的右边。这些原区间也是保留即可。

```c++
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        int i, size = intervals.size(), curLeft, curRight;
        vector<vector<int>> result;
        /*****对于新区间左侧的区间，保持原样**********/
        for (i = 0; i < size; i++)  
        {
            if (intervals[i][1] < newInterval[0])  //当前区间完全在新区间的左边
                result.push_back(intervals[i]);
            else
                break;
        }
        /*****处理与新区间重合的区间**********/
        curLeft = newInterval[0];
        curRight = newInterval[1];
        for (; i < size; i++)  //
        {
            if (intervals[i][1]<curLeft || intervals[i][0]>curRight)  //不重合的情况
                break;
            curLeft = min(intervals[i][0], curLeft);
            curRight = max(intervals[i][1], curRight);
        }
        result.push_back(vector<int>{curLeft, curRight});
        /*****对于新区间右侧的区间，保持原样**********/
        for (; i < size; i++)
        {
            result.push_back(intervals[i]);
        }
        return result;
    }
};

```

