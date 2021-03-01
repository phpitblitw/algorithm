### leetcode_141_easy_环形链表

![image-20210128103401477](leetcode_141_easy_环形链表.assets/image-20210128103401477.png)

![image-20210128103413112](leetcode_141_easy_环形链表.assets/image-20210128103413112.png)

![image-20210128103424533](leetcode_141_easy_环形链表.assets/image-20210128103424533.png)

```c++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        
    }
};
```

#### 算法思路

经典的快慢指针

```c++
class Solution {
public:
	bool hasCycle(ListNode *head) {
		ListNode *pSlow, *pFast;

		pSlow = head;
		pFast = head;
		if (!head)
			return false;
		while (pFast->next && pFast->next->next)
		{
			pSlow = pSlow->next;
			pFast = pFast->next->next;
			if (pSlow == pFast)
				return true;
		}
		return false;
	}
};
```

