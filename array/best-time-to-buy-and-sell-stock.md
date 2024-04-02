# 121.买卖股票的最佳时机

## 题目

给定一个数组 `prices` ，它的第 `i` 个元素 `prices[i]` 表示一支给定股票第 `i` 天的价格。
你只能选择 **某一天** 买入这只股票，并选择在 **未来的某一个不同的日子** 卖出该股票。设计一个算法来计算你所能获取的最大利润。
返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 `0` 。

## 思路

### 1.暴力遍历法

设买入为i，卖出的时间为j，最大利润就是就最大的price[j]-price[i]，注意，卖出的时间必须大于买入的时间，即j>i，
如果最大的price[j]-price[i]仍然小于0，返回0。
此算法复杂度为O(n^2)，提交会超时

### 2.双指针一次遍历法

假设在第i天我们要卖出股票，为了获得最大的利润，我们应该在0~i-1天中的最低价买入，即第i天能获得的最大利润=prices[i]-minPrice

由此，我们可以获得每一天卖出时能获得的最大利润，比较可以得出所能获取的最大利润maxPrice。

声明一个慢指针来记录历史最低价，一个快指针遍历数组处理当前日期

当前日期的最大利润为minPrice = *fast-\*slow

如果minPrice小于零，则当前日期的价格为新的历史最低价,更新历史最低价

#### C

```C
int maxProfit(int* prices, int pricesSize) {
    int fast = 1, slow = 0;
    int maxProfit = 0;
    while(fast < pricesSize)
    {
        if(prices[fast] - prices[slow] > maxProfit)
            maxProfit = prices[fast] - prices[slow];
        if(prices[fast] - prices[slow] < 0)
            slow = fast;
        fast++;
    }
    return maxProfit;
}
```

