### 剑指offer_6_easy_从尾到头打印链表

![image-20210331155208515](剑指offer_6_easy_从尾到头打印链表.assets/image-20210331155208515.png)

```c++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {

    }
};
```

#### 算法思路

```c++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        ListNode *cur;
        vector<int> result;

        cur=head;
        while(cur)
        {
            result.push_back(cur->val);
            cur=cur->next;
        }
        reverse(result.begin(),result.end());
        return result;
    }
};
```

#### 