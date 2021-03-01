### leetcode_99_hard_恢复二叉搜索树

![image-20210113105024811](leetcode_99_hard_%E6%81%A2%E5%A4%8D%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210113105024811.png)

![image-20210113105048182](leetcode_99_hard_%E6%81%A2%E5%A4%8D%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210113105048182.png)

![image-20210113105103451](leetcode_99_hard_%E6%81%A2%E5%A4%8D%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210113105103451.png)

![image-20210113105505182](leetcode_99_hard_%E6%81%A2%E5%A4%8D%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210113105505182.png)

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
    void recoverTree(TreeNode* root) {

    }
};
```

#### 中序遍历法

类比leetcode_98_medium_验证二叉搜索树。二叉搜索树，其中序遍历结果应该是升序的。找到不符合升序的两个节点，交换他们的位置即可

##### 不符合升序的节点

在一个升序数组中，有两个数被交换了位置。在O(n)的复杂度下，如何找到是哪两个数？

将这两个数记为swap1,swap2，有swap1>swap2

例如，在数组nums=[1,2,3,4,7,6,5,8,9]中，swap1=7,swap2=5。

用两个相邻的数组下标i、j来遍历数组。当第一次出现nums[i]>nums[j]时，nums[i]即为swap1。因为

- 对于swap1之前的数，都是有序的。访问这些数，当然nums[i]<nums[j]
- 当访问到下标i指向swap1的位置时，总有nums[i]>nums[j]
  - 如果j指向的元素不是swap2，那么，由于swap1这个数是从后面被交换过来的，那么swap1>nums[j]
  - 如果j指向的元素是swap2，那么swap1>swap2

所以，通过这种方法找到的就是swap1。

类似的，当从后往前遍历 出现nums[i]>nums[j]时，nums[j]即为swap2。



算法的时间复杂度O(n)，包括中序遍历各个节点O(n)，扫描找到两个翻转点O(n)

```c++
class Solution {
public:
	void recoverTree(TreeNode* root) {
		int i,j,pos1,pos2;
		TreeNode *node1, *node2;  //发生交换的两个节点
		vector<TreeNode*> nodes;

		//中序遍历
		inorder(root, nodes);
		//默认初始化
		pos1 = 0;
		pos2 = 0;
		//找到第一个交换的点
		for (i = 0, j = 1; j < nodes.size(); i++,j++)
		{
			if (nodes[i]->val > nodes[j]->val)  //如果顺序相邻的两个节点，val降序，则前面一个节点是第一个交换点
			{
				pos1 = i;
				break;
			}
		}
		//找到第二个交换的点
		for (i=nodes.size()-2, j=nodes.size()-1; i>=0; i--, j--)
		{
			if (nodes[i]->val > nodes[j]->val)  //如果顺序相邻的两个节点，val降序，则后面一个节点是第二个交换点
			{
				pos2 = j;
				break;
			}
		}
		swap(nodes[pos1]->val, nodes[pos2]->val);
	}

	void inorder(TreeNode* root, vector<TreeNode*>& nodes)
	{
		if (root == nullptr)
			return;
		inorder(root->left, nodes);
		nodes.push_back(root);
		inorder(root->right, nodes);
	}
};
```

![image-20210113121951053](leetcode_99_hard_%E6%81%A2%E5%A4%8D%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.assets/image-20210113121951053.png)

#### 常数空间的解决方法

使用两次中序遍历。

第一次，先访问左子树的中序遍历。当前访问到的节点val小于上次访问到的节点val时，找到了第一个翻转点

第二次，先访问右子树的中序遍历。当前访问到的节点val大于上次访问到的节点val时，找到了第二个翻转点

代码略