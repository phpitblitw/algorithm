### leetcode_94_medium_二叉树的中序遍历

![image-20210111144031978](leetcode_94_medium_%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86.assets/image-20210111144031978.png)

![image-20210111144102362](leetcode_94_medium_%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86.assets/image-20210111144102362.png)

![image-20210111144121534](leetcode_94_medium_%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86.assets/image-20210111144121534.png)

![image-20210111144148526](leetcode_94_medium_%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86.assets/image-20210111144148526.png)

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
    vector<int> inorderTraversal(TreeNode* root) {
        
    }
};
```

#### 递归算法

```c++
class Solution {
public:
	vector<int> inorderTraversal(TreeNode* root) {
		vector<int> result;
		inorder(root, result);
		return result;
	}

	//中序遍历
	void inorder(TreeNode *root,vector<int> &result)
	{
		if (root == nullptr)
			return;
		inorder(root->left, result);
		result.push_back(root->val);
		inorder(root->right, result);
	}
};
```

#### 迭代算法

使用指针ListNode* cur 遍历节点，用一个栈stack<ListNode*> 辅助遍历过程。

对于中序遍历，二叉树的每一个节点要经历如下几次访问过程

1. 当cur第一次指向该节点时，由于中序遍历，所以需要优先访问左子树。将该节点入栈，并且将cur指向左子树。
2. 当该节点从栈中被弹出时，cur第二次指向该节点。这意味着该节点的左子树已经被访问完毕。可以访问该节点本身的val
3. 访问该节点的右子树，cur指向右子树

所以，整体的算法流程为

1. 初始化，ListNode* cur=root; 
2. 判断循环终止条件。满足以下其一
   - 指针cur非空，当前节点非空，待访问
   - 栈stk非空，还有节点待访问
3. cur不断指向其左子树，直到cur为nullptr。在此过程中，将节点入栈
4. 当cur为空，弹栈，访问该节点
5. 对于弹栈出的元素，cur再指向其右指针

```c++
class Solution {
public:
	vector<int> inorderTraversal(TreeNode* root) {
		TreeNode *cur;
		stack<TreeNode*> stk;
		vector<int> result;

		cur = root;
		while (cur || !stk.empty())
		{
			//访问最左叶子节点
			while (cur)
			{
				stk.push(cur);
				cur = cur->left;
			}
			//出栈时，访问该节点
			cur = stk.top();
			stk.pop();
			result.push_back(cur->val);
			//添加该节点的右子树
			cur = cur->right;
		}
		return result;
	}
};
```

