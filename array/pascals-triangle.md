# 118.杨辉三角

## 题目

给定一个非负整数 *`numRows`，*生成「杨辉三角」的前 *`numRows`* 行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。

![img](images/1626927345-DZmfxB-PascalTriangleAnimated2.gif)

## 思路

### 方法一：数学

杨辉三角，是二项式系数在三角形中的一种几何排列。它是中国古代数学的杰出研究成果之一，它把二项式系数图形化，把组合数内在的一些代数性质直观地从图形中体现出来，是一种离散型的数与形的结合。

杨辉三角具有以下性质：

1. 每行数字左右对称，由 111 开始逐渐变大再变小，并最终回到 1。
2. 第 n 行（从 0 开始编号）的数字有 n+1项，前 n行共有 n(n+1)/2个数。
3. 每个数字等于上一行的左右两个数字之和，可用此性质写出整个杨辉三角。即第 n行的第 i个数等于第 n−1行的第 i−1 个数和第 i个数之和。

由3我们可以一行一行地把杨辉三角的每一行的数值计算出来。

#### C

```c
int** generate(int numRows, int* returnSize, int** returnColumnSizes) {
    int** ret = malloc(sizeof(int *)* numRows);
    *returnSize = numRows;
    *returnColumnSizes = malloc(sizeof(int) * numRows); 
    for(int i = 0; i < numRows; i++)
    {
        ret[i] = (int*)malloc(sizeof(int) * (i+1));
        (*returnColumnSizes)[i] = i + 1;
        ret[i][0] = ret[i][i] = 1;
        for(int j = 1; j < i;j++)
        {
            ret[i][j] = ret[i-1][j-1] + ret[i-1][j];
        }
    }
    return ret;
}
```

