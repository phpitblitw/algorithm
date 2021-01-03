### leetcode_86_medium_分隔链表

![image-20210103094353908](leetcode_86_medium_分隔链表.assets/image-20210103094353908.png)

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        
    }
};
```

#### 算法思路

维护两个指针。

- 指针pCur，用于向后访问，遍历每个元素，找到小于x的元素。pCur指向已经处理过的最后一个元素
- 指针，pResCur，用于指引应该将小于x的元素插入到什么位置。总是将小于x的元素 插到pResCur的后面

```c++
class Solution {
public:
	ListNode* partition(ListNode* head, int x) {
		ListNode *pCur, *pResCur,*pTemp;
		ListNode *pPreHead;

		pPreHead = new ListNode(INT_MIN);
		pPreHead->next = head;
		//pCur的初始位置，移动到第一个满足pCur->val>=x的地方
		pCur = head;
		pResCur = pPreHead;
		while (pCur&&pCur->val<x)
		{
			pCur = pCur->next;
			pResCur = pResCur->next;
		}
		if (pCur == nullptr)
			return head;
		//将pCur之后的每一个小于x的节点 移动到pCur之前
		while (pCur&&pCur->next)
		{
			if (pCur->next->val < x)  //找到小于x的元素，则将其移动到前面
			{
				pTemp = pResCur->next;
				pResCur->next = pCur->next;  //将节点移动到x之前
				pCur->next = pCur->next->next;  //断开与原位置的连接
				pResCur->next->next = pTemp;  //将节点移动到x之前
				pResCur = pResCur->next;
			}
			pCur = pCur->next;
		}

		pTemp = pPreHead->next;
		delete pPreHead;
		return pTemp;
	}
};
```

