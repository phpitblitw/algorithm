### leetcode_60_hard_排列序列

![image-20201221163125274](leetcode_60_hard_%E6%8E%92%E5%88%97%E5%BA%8F%E5%88%97.assets/image-20201221163125274.png)

```c++
class Solution {
public:
    string getPermutation(int n, int k) {

    }
};
```

#### 算法思路

对于**n位数字**，其可以形成的排列总数为**n!**

同样的，对于n位数字，其后n-1位共有(n-1)!种组合情况。例如，k=(n-1)!*2+1,这也就意味着n位数字的首位为3。

```c++
class Solution {
public:
    string getPermutation(int n, int k) {
        int i,seqNum,j,count,targetSeq;
        vector<int> factorial{ 1,1,2,6,24,120,720,5040,40320,362880 };
        vector<bool> used(n + 1, false);  //[1,n]这些数字是否被使用过 (0仅用于占位 不讨论)
        string result(n,'*');

        k -= 1;  //将k变为下标从0开始
        for (i = 0; i < n; i++)
        {
            seqNum = factorial[n - i - 1];  //[i+1,n-1]这些位置 总共有多少种排列
            targetSeq = int(k / seqNum);  //应该使用第几小的数字(下标从0开始)
            for (j = 1,count=0; j <= n; j++)
            {
                if (used[j])
                    continue;
                if (count == targetSeq)
                {
                    result[i] = '0' + j;
                    used[j] = true;
                    break;
                }
                else
                    count++;
            }
            k = k % seqNum;
        }
        return result;
    }
};
```

