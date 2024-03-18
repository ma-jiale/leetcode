# 两数之和 2024-3-18

## 题目

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** *`target`* 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案

## 思路

按顺序枚举数组中的每一个数x，寻找数组中是否存在等于target-x的数
并且对枚举的x，位于x前面的数以及和它匹配过了，只需要匹配它后面的数

## C

```c
int* twoSum(int* nums, int numsSize, int target, int* returnSize) 
{
    int* ret;
    ret = (int *)malloc(sizeof(int)*2);
    for(int i = 0; i < numsSize - 1; i++)
    {
        for(int j = i + 1; j <  numsSize; j++)
        {
            if(nums[i] + nums[j] == target)
            {
                ret[0] = i;
                ret[1] = j;
                *returnSize = 2;
                return ret;
            }
        }
    }
    *returnSize = 0;
    return NULL;
}
```

