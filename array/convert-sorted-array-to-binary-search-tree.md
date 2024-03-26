# 108.将有序数组转换为二叉树搜索树

## 题目

给你一个整数数组 `nums` ，其中元素已经按 **升序** 排列，请你将其转换为一棵 平衡 二叉搜索树。

## 思路

### 中序遍历，总是选择中间位置或中间位置左边的数字作为根节点

为了保持树的高度平衡，我们可以选择中间位置（数组长度为奇数）或中间位置左边的数字（数组长度为偶数）作为根节点，因为nums严格递增，左子树的所有元素都在作为根节点数字的左边；右子树的所有元素都在作为根节点数字的右边。同样为了保持树的高度平衡，左子树和右子树分别也是平衡二叉搜索树，因此可以使用递增的方式建立平衡二叉树搜索树。

递归的基准情形是平衡二叉搜索树不包含任何数字，此时平衡二叉搜索树为空。

在给定中序遍历序列数组的情况下，每一个子树中的数字在数组中一定是连续的，因此可以通过数组下标范围确定子树包含的数字，下标范围记为[left,right]，对于整个中序遍历序列，下标范围left = 0到right = nums.length - 1, left>right时，平衡二叉搜索树为空。

#### C

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
struct TreeNode* buildBST(int * nums, int left, int right)
{
    if(left > right)
        return NULL;
    int middle = (left + right)/2;
    struct TreeNode* root = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    root->val = nums[middle];
    root->left = buildBST(nums, left, middle - 1);
    root->right = buildBST(nums, middle + 1, right);
    return root;
}

struct TreeNode* sortedArrayToBST(int* nums, int numsSize) {
    return buildBST(nums, 0, numsSize - 1);
}
```

