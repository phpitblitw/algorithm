### leetcode_104_easy_二叉树的最大深度

![image-20210113170954514](leetcode_104_easy_%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6.assets/image-20210113170954514.png)

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
    int maxDepth(TreeNode* root) {

    }
};
```

#### 算法思路

max(左子树最大深度，右子树最大深度)+1

```c++
class Solution {
public:
	int maxDepth(TreeNode* root) {
		if (root == nullptr)
			return 0;
		else
			return max(maxDepth(root->left), maxDepth(root->right)) + 1;
	}
};
```

