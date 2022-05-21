## 题目

> **示例 1：**
>
> ```
> 输入：root = [4,2,7,1,3,6,9]
> 输出：[4,7,2,9,6,3,1]
> ```



## 实现一

使用递归的方式实现。

```c++
TreeNode* mirrorTree(TreeNode* root)
{
    if(nullptr == root)
    {
        return nullptr;
    }
    TreeNode* pTmp = root->left;
    root->left = mirrorTree(root->right);
    root->right = mirrorTree(pTmp);
    return root;
}
```



## 实现二

将递归改为使用栈的方式

```c++
TreeNode* mirrorTree(TreeNode* root)
{
    if(nullptr == root)
    {
        return nullptr;
    }
    stack<TreeNode*> s;
    s.push(root);
    while(!s.empty())
    {
        TreeNode* pRoot = s.top();
        s.pop();
        TreeNode* pTmp = pRoot->left;
        pRoot->left = pRoot->right;
        pRoot->right = pTmp;
        if(nullptr != pRoot->left)
        {
            s.push(pRoot->left);
        }
        if(nullptr != pRoot->right)
        {
            s.push(pRoot->right);
		}
    }
    return root;
}
```

