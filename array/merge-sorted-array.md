# 88.合并两个有序数组2024.3.25

## 题目

给你两个按 **非递减顺序** 排列的整数数组 `nums1` 和 `nums2`，另有两个整数 `m` 和 `n` ，分别表示 `nums1` 和 `nums2` 中的元素数目。

请你 **合并** `nums2` 到 `nums1` 中，使合并后的数组同样按 **非递减顺序** 排列。

**注意：**最终，合并后数组不应由函数返回，而是存储在数组 `nums1` 中。为了应对这种情况，`nums1` 的初始长度为 `m + n`，其中前 `m` 个元素表示应合并的元素，后 `n` 个元素为 `0` ，应忽略。`nums2` 的长度为 `n` 。

## 思路

### 合并后排序

将两个数组合并后，对整个数组排序即可

### 双指针

如果nums2长度为0，直接返回nums1;
如果nums2长度不为0，可以声明一个长度为m+n的临时数组sorted[m+n]，和两个快指针fast1,fast2,
fast1指针遍历nums1,fast2指针遍历nums2,快指针用来将两个数组的元素重新排序，慢指针用来建立输出数组
快指针指向sorted数组当前需要处理的元素，慢指针指向下一个需要赋值的位置
1.当nums1[fast1]<nums2[fast2]时，将nums1[fast1]赋给sorted[slow],并递增fast1,slow;
2.当nums1[fast1]>nums2[fast2]时，将nums2[fast2]赋给sorted[slow],并递增fast2,slow;
3.当nums1[fast1]=nums2[fast2]时，按照情况一处理。
当fast1 = m，或者fast2 = n时，将另一个数组的剩余元素赋给临时数组即可。
为什么使用临时数组存放排序结果，而不是直接更新在nums1上？
因为nums1的元素可能还没有使用就会被排序好的元素覆盖掉，如nums1 = {3,4,4,5},nums2 = {1,2,2,3}。

### C

```
void merge(int* nums1, int nums1Size, int m, int* nums2, int nums2Size, int n) {
    int fast1 = 0, fast2 = 0;
    int slow = 0;
    int sorted[m + n];
    while(fast1 < m || fast2 < n)
    {
        if(fast1 == m)
        {
            sorted[slow++] = nums2[fast2++];
        }
        else if(fast2 == n)
        {
            sorted[slow++] = nums1[fast1++];
        }
        else if(nums1[fast1] <= nums2[fast2])
        {
            sorted[slow++] = nums1[fast1++];
        }
        else
        {
            sorted[slow++] = nums2[fast2++];
        }
    }
    for(int i = 0; i < m+n; i++)
        nums1[i] = sorted[i];
}
```

