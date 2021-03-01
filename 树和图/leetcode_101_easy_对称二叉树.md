### leetcode_101_easy_对称二叉树

![image-20210113144208810](leetcode_101_easy_%E5%AF%B9%E7%A7%B0%E4%BA%8C%E5%8F%89%E6%A0%91.assets/image-20210113144208810.png)

![image-20210113144219886](leetcode_101_easy_%E5%AF%B9%E7%A7%B0%E4%BA%8C%E5%8F%89%E6%A0%91.assets/image-20210113144219886.png)

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
    bool isSymmetric(TreeNode* root) {
        
    }
};
```

#### 递归法

辅助函数isSymmetric(TreeNode* root1,TreeNode* root2)，判断两棵树root1,root2是否对称。则原问题转化为判断root->left,root->right这两棵子树是否对称

辅助函数isSymmetric()的判断逻辑如下：

- 判断根节点的值是否相等
- 判断root1的左子树和root2的右子树是否对称
- 判断root1的右子树和root2的左子树是否对称

```c++
class Solution {
public:
	bool isSymmetric(TreeNode* root) {
		if (root == nullptr)
			return true;
		else
			return isSymmetric(root->left, root->right);
	}

	bool isSymmetric(TreeNode* root1, TreeNode* root2)
	{
		if (root1 == nullptr && root2 == nullptr)
			return true;
		else if (root1 == nullptr || root2 == nullptr)
			return false;
		else if (root1->val != root2->val)
			return false;
		else
			return isSymmetric(root1->left, root2->right)
			&& isSymmetric(root1->right, root2->left);
	}
};
```

#### 迭代法

对于root的两棵子树root->left和root->right，比较他们是否对称。

对于root->left，对它进行**先访问左子树的中序遍历**。

对于root->right，对它进行**先访问右子树的中序遍历**。

如果root->left和root->right这两棵树对称，则以上两种遍历的结果应该相同。

以上遍历用队列来实现。

```
class Solution {
public:
	bool isSymmetric(TreeNode* root) {
		TreeNode *n1, *n2;
		queue<TreeNode*> q1, q2;
		if (root == nullptr)
			return true;
		q1.push(root->left);  //左子树
		q2.push(root->right);  //右子树
		while (!q1.empty() && !q2.empty())
		{
			n1 = q1.front();
			n2 = q2.front();
			q1.pop();
			q2.pop();
			if (n1 == nullptr&&n2 == nullptr)
				continue;
			else if (n1 == nullptr || n2 == nullptr)
				return false;
			else if (n1->val != n2->val)
				return false;
			//对root->left这棵树，进行先访问左子树的中序遍历
			q1.push(n1->left);
			q1.push(n1->right);
			//对root->right这棵树，进行先访问右子树的中序遍历
			q2.push(n2->right);
			q2.push(n2->left);
		}
		if (!q1.empty() || !q2.empty())
			return false;
		else
			return true;
	}
};
```

