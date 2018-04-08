## LeetCode 121 Best Time to Buy and Sell Stock

### Problem:

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

**Example 1:**

```python
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```

**Example 2:**

```python
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.
```



### Solution:

Brute-Force approach will get **Time Limit Exceeded Error**, so another one-pass approach is appreciated here:

```python
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        n = len(prices)
        if(n < 2):
            return 0
        min_price = prices[0]
        max_profit = 0
        for i in range(1,n):
            min_price = min(min_price,prices[i])
            max_profit = max(max_profit,prices[i] - min_price)
        return max_profit
```



