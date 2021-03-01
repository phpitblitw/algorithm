### leetcode_95_medium_不同的二叉搜索树

![image-20210111154415298](leetcode_95_medium_%E4%B8%8D%E5%90%8C%E7%9A%84%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210111154415298.png)

![image-20210111154431412](leetcode_95_medium_%E4%B8%8D%E5%90%8C%E7%9A%84%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210111154456099.png)

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
    vector<TreeNode*> generateTrees(int n) {
        
    }
};
```

#### 算法思路

使用**递归**的思想，将原问题转变为规模更小的子问题，处理子问题的解。

定义generateTrees(start,end) 表示，处理[start,end]区间所能够生成的所有二叉搜索树。则该问题可以划归为规模更小的子问题。以mid作为根节点，以[start,mid-1]区间生成左子树，以[mid+1,end]区间生成右子树

```c++
class Solution {
public:
	vector<TreeNode*> generateTrees(int n) {
		if (n <= 0)
			return {};
		return generateTrees(1, n);
	}

	vector<TreeNode*> generateTrees(int start, int end)
	{
		int mid,i,j;
		TreeNode* root;
		vector<TreeNode*> result,leftTrees,rightTrees;
		if (start > end)
			return { nullptr };
		for (mid = start; mid <= end; mid++)
		{
			leftTrees = generateTrees(start, mid - 1);
			rightTrees = generateTrees(mid + 1, end);
			for (i = 0; i < leftTrees.size(); i++)
			{
				for (j = 0; j < rightTrees.size(); j++)
				{
					root = new TreeNode(mid);
					root->left = leftTrees[i];
					root->right = rightTrees[j];
					result.push_back(root);
				}
			}
		}
		return result;
	}
};
```

![image-20210111160116955](leetcode_95_medium_%E4%B8%8D%E5%90%8C%E7%9A%84%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210111160116955.png)