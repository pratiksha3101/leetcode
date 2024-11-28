# Maximum Subarray Problem

## Problem Description
The Maximum Subarray problem involves finding the contiguous subarray with the largest sum within a given array of integers. This is a classic algorithmic problem with multiple solution approaches.

## LeetCode Problem
- **Problem Link**: [Maximum Subarray on LeetCode](https://leetcode.com/problems/maximum-subarray/)
- **Difficulty**: Medium

## Solution Approaches

### 1. Brute Force Approach
- **Time Complexity**: O(n³)
- **Space Complexity**: O(1)
- **Approach**: 
  - Use three nested loops to generate all possible subarrays
  - Calculate the sum of each subarray
  - Keep track of the maximum sum encountered
- **Pros**: Simple to implement
- **Cons**: Extremely inefficient for large arrays

### 2. Better Approach
- **Time Complexity**: O(n²)
- **Space Complexity**: O(1)
- **Approach**:
  - Use two nested loops
  - Optimize by maintaining a running sum for each subarray
  - Update maximum sum as you go
- **Pros**: Improved efficiency compared to brute force
- **Cons**: Still quadratic time complexity

### 3. Optimal Approach: Kadane's Algorithm
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)
- **Approach**:
  - Iterate through the array once
  - Maintain two variables: 
    1. `currSum`: current running sum of the subarray
    2. `maxSum`: maximum sum found so far
  - Key steps:
    - Add current element to `currSum`
    - Update `maxSum` if `currSum` is larger
    - If `currSum` becomes negative, reset it to 0

#### Kadane's Algorithm Explanation
Kadane's algorithm is an elegant dynamic programming approach that solves the maximum subarray problem efficiently. The core idea is to:
- Always keep track of the maximum sum seen so far
- Reset the current sum to 0 if it becomes negative
- This allows us to "drop" subarrays that would decrease our overall sum

**Key Insights**:
- If adding an element makes the current sum negative, it's better to start a new subarray
- The algorithm effectively finds the most profitable contiguous sequence
- Works well with both positive and negative numbers

## Code Examples
```go
// Optimal solution using Kadane's Algorithm
// When your current life situation (current sum) becomes negative or detrimental, it's better to reset to zero (start over) rather than continuing down a destructive path.
func maxSubArray(nums []int) int {
    currSum := 0
    maxSum := math.MinInt

    for _, v := range nums {
        currSum += v

        if currSum > maxSum {
            maxSum = currSum
        }

        if currSum < 0 {
            currSum = 0
        }
    }

    return maxSum
}
```

## Real-world Applications
- Financial analysis (finding the most profitable period)
- Signal processing
- Image processing
- Optimization problems in various domains

## Time and Space Complexity Comparison
| Approach   | Time Complexity | Space Complexity |
|------------|----------------|------------------|
| Brute Force | O(n³)          | O(1)             |
| Better     | O(n²)          | O(1)             |
| Optimal    | O(n)           | O(1)             |
