### leetcode_102_medium_二叉树的层序遍历

![image-20210113152501209](leetcode_102_medium_%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.assets/image-20210113152501209.png)

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        
    }
};
```

#### 算法思路

先序遍历

维护2个变量，nodeNumCur当前行的节点数量(不含空节点)，nodeNumNext下一行的节点数量(不含空节点)。每次访问到一个节点，nodeNumCur--。每次为队列添加一个节点，nodeNumNext++。

```c++
class Solution {
public:
	vector<vector<int>> levelOrder(TreeNode* root) {
		int nodeNumCur, nodeNumNext;
		TreeNode *curNode;
		queue<TreeNode*> q;
		vector<int> curLine;
		vector<vector<int>> result;

		if (root == nullptr)
			return result;
		//首行
		nodeNumCur = 1;
		nodeNumNext = 0;
		q.push(root);
		//先序遍历
		while (!q.empty())
		{
			if (nodeNumCur == 0)  //如果这行的元素访问完了，转到下一行
			{
				result.push_back(curLine);
				curLine.clear();
				nodeNumCur = nodeNumNext;
				nodeNumNext = 0;
			}
			else  //这行还没访问完
			{
				curNode = q.front();
				q.pop();
				nodeNumCur--;
				curLine.push_back(curNode->val);
				if (curNode->left)
				{
					nodeNumNext++;
					q.push(curNode->left);
				}
				if (curNode->right)
				{
					nodeNumNext++;
					q.push(curNode->right);
				}
			}
		}
		if (!curLine.empty())
			result.push_back(curLine);
		return result;
	}
};
```

