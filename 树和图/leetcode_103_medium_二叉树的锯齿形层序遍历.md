### leetcode_103_medium_二叉树的锯齿形层序遍历

![image-20210113155933345](leetcode_103_medium_%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%94%AF%E9%BD%BF%E5%BD%A2%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.assets/image-20210113155933345.png)

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        
    }
};
```

#### 算法思路

类似leetcode_102_medium_二叉树的层序遍历。

用题解的方法，而非102中我的方法，重写题目

添加了一个标记量bool inorder，标记改行按照正序/逆序遍历

```c++
class Solution {
public:
	vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
		bool inorder;  //该行是否按正序遍历
		int i, curLineSize;
		TreeNode* curNode;
		queue<TreeNode*> q;
		vector<int> curLineData;
		vector<vector<int>> result;

		if (root == nullptr)
			return result;
		q.push(root);
		inorder = true;
		while (!q.empty())
		{
			curLineData.clear();
			curLineSize = q.size();  //当前行的长度
			for (i = 0; i < curLineSize; i++)  //访问当前行的每一个元素
			{
				curNode = q.front();
				q.pop();
				curLineData.push_back(curNode->val);
				if (curNode->left)
					q.push(curNode->left);
				if (curNode->right)
					q.push(curNode->right);
			}
			if (!inorder)
				reverse(curLineData.begin(), curLineData.end());
			inorder = !inorder;
			result.push_back(curLineData);
		}
		return result;
	}
};
```

