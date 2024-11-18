# Best Time to Buy and Sell Stock

## Problem
[LeetCode Problem Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

## Solution (Go)

```go
// Time Complexity: O(n)
// Space Complexity: O(1)
func maxProfit(prices []int) int {
    profit := 0
    minPrice := prices[0]

    for i := 1; i < len(prices); i++ {
        if prices[i] < minPrice {
            minPrice = prices[i]  // buying
        } else if prices[i] - minPrice > profit {
            profit = prices[i] - minPrice
        }
    }

    return profit
}
```

## Approach
- Iterate through the prices array
- Keep track of the minimum price seen so far
- Calculate maximum potential profit at each step
- Return the maximum profit

## Complexity
- **Time Complexity**: O(n), where n is the number of prices
- **Space Complexity**: O(1), using only two variables

## Example
```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5
```
