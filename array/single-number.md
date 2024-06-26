# 136.只出现一次的数字2024.3.29

## 题目

给你一个 **非空** 整数数组 `nums` ，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

你必须设计并实现线性时间复杂度的算法来解决此问题，且该算法只使用常量额外空间。

## 思路

### 方法一：位运算（异或）

异或运算有以下三个性质。
任何数和 000 做异或运算，结果仍然是原来的数，即 a⊕0=a
任何数和其自身做异或运算，结果是 000，即 a⊕a=0
异或运算满足交换律和结合律，即 a⊕b⊕a=b⊕a⊕a=b⊕(a⊕a)=b⊕0=b

![img](images/3.PNG)

假设数组中有2m+1 个元素，其中有 m 个数各出现两次，一个数出现一次。其中设a(m+1)为唯一出现一次的数。对所有的元素做异或运算，根据异或运算满足交换律和结合律，可将原式变换为

(*a*1⊕*a*1)⊕(*a*2⊕*a*2)⊕⋯⊕(am*⊕*am)⊕a(m+1)

再根据异或运算的1，2性质，化简式子的

a(m+1)，及唯一出现的元素。