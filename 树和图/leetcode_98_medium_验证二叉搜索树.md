### leetcode_98_medium_验证二叉搜索树

![image-20210113101602092](leetcode_98_medium_%E9%AA%8C%E8%AF%81%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210113101602092.png)

![image-20210113101616396](leetcode_98_medium_%E9%AA%8C%E8%AF%81%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210113101616396.png)

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
    bool isValidBST(TreeNode* root) {

    }
};
```

#### 算法思路

把原问题拆解为规模更小的子问题，**递归**地解决

判断树root是否为二叉搜索树，且节点val在[min,max]之间，即为

- 判断左子树root->left是否为二叉搜索树，且节点val在[min,root->val-1]之间
- 判断左子树root->right是否为二叉搜索树，且节点val在[root->val+1,max]之间



另外，root->val-1这样的操作，可能会引起**越界**。因此，需要单独处理如root->val==INT_MIN或者root->val==INT_MAX这样的情况。

- 当root->val==INT_MIN，左子树不应有任何节点
- 当root->val==INT_MAX，右子树不应有任何节点

```c++
class Solution {
public:
	bool isValidBST(TreeNode* root) {
		return isValid(root, INT_MIN, INT_MAX);
	}

	//判断树root是否为二叉搜索树，且节点val在[min,max]之间
	bool isValid(TreeNode *root, int min, int max)
	{
		bool result = true;
		//空树总是合法的
		if (root == nullptr)
			return true;
		//判断根节点val是否合法
		if (root->val<min || root->val>max)
			return false;
		//判断左子树是否合法
		if (root->val == INT_MIN)
			result = result && (root->left == nullptr);
		else
			result = result&&isValid(root->left, min, root->val - 1);
		//判断右子树是否合法
		if (root->val == INT_MAX)
			result = result && root->right == nullptr;
		else
			result = result && isValid(root->right, root->val + 1, max);
		
		return result;
	}
};
```

#### 中序遍历

二叉搜索树，其中序遍历结果应该是递增的

代码略