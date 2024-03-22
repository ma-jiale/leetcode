# 27.移除元素

## 题目

给你一个数组 `nums` 和一个值 `val`，你需要 **[原地](https://baike.baidu.com/item/原地算法)** 移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 `O(1)` 额外空间并 **[原地 ](https://baike.baidu.com/item/原地算法)修改输入数组**。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

## 思路

### 双指针

定义一个快指针fast和一个慢指针slow，将所有不等于val的值重新排列起来形成输出数组
fast指针遍历数组的每个元素，检查元素是否等于val，slow指针用来建立输出数组
fast指针指向当前需要处理的元素，slow指针指向下一个需要赋值的位置
1.若fast指向的值不等于val，该值在输出数组内，将该值赋给slow指向的位置。递增fast和slow指针，
2.若fast指向的值等于val，该值不在输出数组内，递增fast指针，slow指针保持不变。
slow的值等于输出数组元素的个数，返回slow的值

## C

```c
int removeElement(int* nums, int numsSize, int val) {
    int fast = 0,slow = 0;
    for(int i = 0; i < numsSize; i++)
    {
        if(nums[fast] != val)
        {
            nums[slow] = nums[fast];
            slow++;
        }
        fast++;
    }
    return slow;
}
```

