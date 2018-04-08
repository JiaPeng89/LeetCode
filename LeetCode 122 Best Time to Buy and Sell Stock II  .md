## LeetCode 122 Best Time to Buy and Sell Stock II

### Problem:

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).



### Solution:

at first, I'm busy checking the valleys and peaks:

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
        profit = 0
        for i in range(1,n-1):
            if(prices[i] > min_price and prices[i] > prices[i+1]):
                profit += prices[i] - min_price
                min_price = prices[i+1]
            else:
                min_price = min(min_price,prices[i])
        if(prices[n-1] > min_price):
            profit += prices[n-1] - min_price
        return profit
```

and then I'm a little excited that these consecutive profits can be accumulated and make no difference about the total profit!

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
        
        profit = 0
        for i in range(1,n):
            if(prices[i] - prices[i-1] > 0):
                profit += prices[i] - prices[i-1]
        return profit
```

