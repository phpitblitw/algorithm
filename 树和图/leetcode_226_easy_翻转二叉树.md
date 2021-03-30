### leetcode_226_easy_翻转二叉树

![image-20210323154827581](leetcode_226_easy_翻转二叉树.assets/image-20210323154827581.png)

```c++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {

    }
};
```

#### 算法思路

递归地进行翻转

```c++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root!=nullptr)
        {
            root->left=invertTree(root->left);
            root->right=invertTree(root->right);
            swap(root->left,root->right);
        }
        return root;
    }
};
```

