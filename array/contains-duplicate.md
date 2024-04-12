# 217.存在重复元素

## 题目

给你一个整数数组 `nums` 。如果任一值在数组中出现 **至少两次** ，返回 `true` ；如果数组中每个元素互不相同，返回 `false` 。

## 思路

### 排序

对数组进行排序，重复的元素一定在排序后数组中相邻。可以遍历排序后数组元素，判断相邻的元素是否相等的，如果相等则说明有重复元素，返回true，否则返回false。

#### c

```
int cmp(const int* a, const int* b)
{
    return (*(int*)a - *(int*)b);
}

bool containsDuplicate(int* nums, int numsSize) 
{
    qsort(nums, numsSize, sizeof(int), cmp);
    for(int i = 0; i < numsSize-1; i++)
    {
        if(nums[i] == nums[i+1])
            return true;
    }
    return false;
}
```

