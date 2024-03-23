# 35.搜索插入位置2024.3.23

## 题目

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 `O(log n)` 的算法。

## 思路

### 1.暴力求解法

1.目标值存在于数组中，遍历数组返回相应数组下标

2.目标值不存在于数组中时，可分为

- 目标值在数组首元素和最后一个元素之间，遍历数组，当num[i-1]<target<nums[i]时，返回i
- 目标值小于数组首元素，返回0
- 目标值大于数组最后一个元素，返回数组大小

C

```c
int searchInsert(int* nums, int numsSize, int target) 
{
    if(target < nums[0])
        return 0;
    if(target > nums[numsSize - 1])
        return numsSize;
    for(int i = 0; i < numsSize; i++)
    {
        if(nums[i] == target)
            return i;
    }
    for(int j = 1; j < numsSize; j++)
    {
        if(target > nums[j-1] && target < nums[j])
            return j;
    }
    return -1;
}
```

