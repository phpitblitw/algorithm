### 剑指offer_10.1_easy_斐波那契数列

![image-20210331163546469](剑指offer_10.1_easy_斐波那契数列.assets/image-20210331163546469.png)

```c++
class Solution {
public:
    int fib(int n) {

    }
};
```

#### 算法思路

dp作斐波那契数列，控制时间复杂度O(1)

```c++
class Solution {
public:
    int fib(int n) {
        int i,fformer,former,cur;  //前1个 前2个元素
        static int DIVISOR=1000000007;
        
        if(n==0)
            return 0;
        else if(n==1)
            return 1;
        fformer=0;
        former=1;
        for(i=2;i<=n;i++)
        {
            cur=fformer+former;
            if(cur>DIVISOR)
                cur=cur%DIVISOR;
            fformer=former;
            former=cur;
        }
        return former;
    }
};
```

