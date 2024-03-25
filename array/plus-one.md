# 66.加一

## 题目

给定一个由 **整数** 组成的 **非空** 数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储**单个**数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

## 思路

要给整数+1时，考虑是否需要进位，可以分为三种情况

1. 如果数组末尾不等于9，直接给数组末尾元素+1并返回数组即可
2. 如果数组末尾有多个9但第一位不为9，需要从后向前找到不等于9的元素，给它+1，并将它后面的元素设为0，返回数组
3. 如果数组所有元素都等于9，则需要构建一个比该数组大小大一位的数组，其首位位1，其余位置为0，返回新的数组

由此，我们需要倒序遍历数组，找到第一个不为9的元素，将它设为1，将它后面的元素全部设为0，返回该数组，如果数组元素全部都是9，则新建立一个比原数组多一位的新数组，将新数组的第一位设为1，其余为设为0，返回新数组。

### c

```
int* plusOne(int* digits, int digitsSize, int* returnSize) {
    for(int i = digitsSize - 1; i >= 0; i--)
    {
        if(digits[i] != 9)
        {
            digits[i]++;
            for(int j = i + 1; j < digitsSize; j++)
            {
                digits[j] = 0;
            }
            *returnSize = digitsSize;
            return digits;
        }
    }
    int * ans;
    ans = (int *)calloc((digitsSize+1), sizeof(int));
    ans[0] = 1;
    *returnSize = digitsSize + 1;
    return ans;
}
```

