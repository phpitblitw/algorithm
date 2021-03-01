### leetcode_100_easy_相同的树

![image-20210113143204665](leetcode_100_easy_%E7%9B%B8%E5%90%8C%E7%9A%84%E6%A0%91.assets/image-20210113143204665.png)

![image-20210113143217049](leetcode_100_easy_%E7%9B%B8%E5%90%8C%E7%9A%84%E6%A0%91.assets/image-20210113143217049.png)

![image-20210113143228035](leetcode_100_easy_%E7%9B%B8%E5%90%8C%E7%9A%84%E6%A0%91.assets/image-20210113143228035.png)

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {

    }
};
```

#### 算法思路

递归+深度优先搜索

判断两个二叉树是否相同，即判断：

- 根节点是否相同
- 左子树是否相同
- 右子树是否相同

```c++
class Solution {
public:
	bool isSameTree(TreeNode* p, TreeNode* q) {
		//根节点是否相同
		if (p == nullptr && q == nullptr)
			return true;
		else if (p == nullptr || q == nullptr)
			return false;
		else if (p->val != q->val)
			return false;
		//左子树是否相同
		if (!isSameTree(p->left, q->left))
			return false;
		//右子树是否相同
		if (!isSameTree(p->right, q->right))
			return false;

		return true;
	}
};
```

