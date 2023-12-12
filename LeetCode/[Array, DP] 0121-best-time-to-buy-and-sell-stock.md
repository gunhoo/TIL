> LeetCode - 121. Best Time to Buy and Sell Stock <a href="https://leetcode.com/problems/best-time-to-buy-and-sell-stock/">Source</a> - Easy

## Problem
You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

## Solution
### Easy Approach - Brute Force
You can set max value as MIN_VALUE at first. While iterating through the for loop twice, it is possible to compare the current and next value, subtract them, and then compare the result with the max value to update the maximum value.

Time Complexity $$O(n^2)$$

### My Approach -  One Pass
```java
class Solution {
    public int maxProfit(int[] prices) {
        int min = prices[0];
        int max = 0;
        for(int i = 0; i < prices.length; i++){
            int cur = prices[i];
            if (cur < min) {
                min = cur;
            } else {
                max = Math.max(max, cur-min);
            }
        }
        return max;
    }
}
```
While iterating through the for loop, you can obtain the minimum value. If the min value is not updated, you can then compare the difference between the current value and the minimum value with the maximum value obtained so far to update the miximum value.

## Time Complexity
$$O(n)$$

## Related Topics
- Array
- Dynamic Programming

## Companies
- Amazon(37)
- Apple(12)
- Adobe(11)
- Microsoft(10)
- Yandex(8)
- Google(7)
- Bloomberg(5)
- Zoho(5)
- Media.net(5)
- Facebook(4)
- Nvidia(4)
- IBM(4)