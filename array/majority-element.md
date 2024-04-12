# 169.多数元素

## 1.题目

给定一个大小为 `n` 的数组 `nums` ，返回其中的多数元素。多数元素是指在数组中出现次数 **大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

## 2.思路

### 1.排序

数组nums有n个元素，如果将数组nums的所有元素按照单调递增或者单调递减排序，则下标为n/2的元素一定是**多数元素**。（下标从0开始）

因为多数元素的个数至少为n/2+1个，考虑排序后数组中多数元素位置的极限情况，即多数元素全在最前面和最后面时，下标为n/2的元素是否为**多数元素**。

#### c

```
int compare(const void *a, const void *b) 
{
    return (*(int*)a - *(int*)b);
}

int majorityElement(int* nums, int numsSize) 
{
    qsort(nums, numsSize, sizeof(int), compare);
    return nums[numsSize/2];
}
```



### 2.暴力算法

最简单的暴力方法是，枚举数组中的每个元素，再遍历一遍数组统计其出现次数。该方法的时间复杂度是 O(n2)

