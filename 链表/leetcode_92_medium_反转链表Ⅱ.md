### leetcode_92_medium_反转链表Ⅱ

![image-20210110151441497](leetcode_92_medium_%E5%8F%8D%E8%BD%AC%E9%93%BE%E8%A1%A8%E2%85%A1.assets/image-20210110151441497.png)

```c++
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        
    }
};
```

#### 算法思路

主要参考笔记**翻转链表.md**

参考题解https://leetcode-cn.com/problems/reverse-linked-list-ii/solution/shuang-100die-dai-fa-tong-su-yi-dong-by-tcl_love/

翻转[m,n]这样一个子链表

```c++
class Solution {
public:
	ListNode* reverseBetween(ListNode* head, int m, int n) {
		int count;
		ListNode* cur;
		ListNode * prehead = new ListNode(-1);
		prehead->next = head;  //虚假的头结点
		cur = prehead;
		//令cur指向m前面的一个节点
		count = 1;
		while (count<m)
		{
			cur = cur->next;
			count++;
		}
		//翻转部分链表
		cur->next = this->reverse(cur->next, n - m + 1);
		return prehead->next;
		return nullptr;
	}

	//翻转从head开始的num个节点。返回新链表的头结点
	ListNode * reverse(ListNode * head, int num)
	{
		int i;
		ListNode *prev, *cur, *nxt;

		prev = nullptr;
		cur = head;
		nxt = head->next;  //不失一般性，为nxt赋初值
		//分别翻转每一个节点
		for (i = 0; i < num; i++)
		{
			nxt = cur->next;
			cur->next = prev;
			prev = cur;
			cur = nxt;
		}
		//与原链表的后面部分相拼接
		head->next = nxt;
		return prev;
	}
};
```

