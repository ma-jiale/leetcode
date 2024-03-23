# 4.寻找两个正序数组中的中位数 2024.3.20

## 题目

给定两个大小分别为 `m` 和 `n` 的正序（从小到大）数组 `nums1` 和 `nums2`。请你找出并返回这两个正序数组的 **中位数** 。

算法的时间复杂度应该为 `O(log (m+n))` 。

## 思路

### 二分查找

对于一组m个数的有序数来说，若m为奇数，中位数是第m/2+1个数，若m为偶数，中位数是第m/2和第m/2+1的和的一半。/为整除
所以可以将寻找中位数转化为寻找一组数中的第k个数，k = m/2或k = m/2 + 1。

对于此题，并不需要将两个数组合并排序，可以写一个从两个正序数组中寻找第k个数的函数。

将nums1[k/2-1]和nums2[k/2-1]，若nums1[k/2-1]小于nums2[k/2-1]，则nums1[k/2-1]一定不是第k个数，因为它前面最多有(k/2-1)*2 个数，此时就可以排除nums1[0]到nums1[k/2-1]个数（k/2个数），查找范围缩小了一半。
因此我们可以归纳出三种情况：

若nums1[k/2-1]小于nums2[k/2-1]， 排除nums1[0]到nums1[k/2-1]
若nums1[k/2-1]大于nums2[k/2-1]，排除nums2[0]到nums2[k/2-1]
若nums1[k/2-1]等于nums2[k/2-1]，我们归为第一种情况处理

接着我们将本轮被排除数组的首项已到被排除数的下一项，并根据排除情况更新k(因为我们要寻找第k个数，在排除数后产生的新数组对中，原第k个数变为第k-排除数个数个数)

继续对新的数组进行上述操作，知道找到原第k个数

![fig1](images/4_fig1.png)

C

```c
int min(int x, int y)
{
    return x <= y ? x : y;
}
int getKthElement(int* nums1, int m, int* nums2, int n, int k)
{
    int index1 = 0, index2 = 0;
    while(1)
    {
        //处理特殊情况
        if (index1 == m) 
        {
            return nums2[index2 + k - 1];
        }
        if (index2 == n) 
        {
            return nums1[index1 + k - 1];
        }
        //同时也是普通情况的出口
        if (k == 1) 
            return min(nums1[index1], nums2[index2]);
		//处理普通情况
        int newIndex1 = min(index1 + k / 2 - 1, m - 1);//防止数组下标越界
        int newIndex2 = min(index2 + k / 2 - 1, n - 1);//防止数组下标越界
        if(nums1[newIndex1] <= nums2[newIndex2])
        {
            k = k - (newIndex1 - index1 + 1);
            index1 = newIndex1 + 1;
        }
        else
        {
            k = k - (newIndex2 - index2 + 1);
            index2 = newIndex2 + 1;
        }
    }
}

double findMedianSortedArrays(int* nums1, int nums1Size, int* nums2, int nums2Size) 
{
    int size = nums1Size + nums2Size;
    if(size % 2 == 0)
        return (getKthElement(nums1, nums1Size, nums2, nums2Size, size/2 + 1) + getKthElement(nums1, nums1Size, nums2, nums2Size, size/2))/2.0;
    else 
        return getKthElement(nums1, nums1Size, nums2, nums2Size, size/2 + 1);
}
```

