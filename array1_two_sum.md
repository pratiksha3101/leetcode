# Two Sum

## Problem Description
[LeetCode Problem #1](https://leetcode.com/problems/two-sum/)

Given an array of integers `nums` and an integer `target`, return indices of the two numbers in the array such that they add up to `target`. You may assume that each input would have exactly one solution, and you may not use the same element twice.

## Problem Constraints
- 2 ≤ nums.length ≤ 10⁴
- -10⁹ ≤ nums[i] ≤ 10⁹
- -10⁹ ≤ target ≤ 10⁹
- Only one valid answer exists

## Examples

### Example 1:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1]
```

### Example 2:
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

### Example 3:
```
Input: nums = [3,3], target = 6
Output: [0,1]
```

## Solutions

### 1. Brute Force Approach
```go
func approach1(nums []int, target int) []int {
    for i := 0; i < len(nums)-1; i++ {
        for j := i + 1; j < len(nums); j++ {
            if nums[i] + nums[j] == target {
                return []int{i, j} 
            }
        }
    }
    return nil  
}
```

**Complexity Analysis:**
- Time Complexity: O(n²)
  - Uses nested loops to check every possible pair
- Space Complexity: O(1)
  - Uses constant extra space

### 2. Hash Map Approach
```go
func approach2(nums []int, target int) []int {
    numMap := make(map[int]int)
    for i, num := range nums {
        complement := target - num
        if j, exists := numMap[complement]; exists {
            return []int{j, i}
        }
        numMap[num] = i
    }
    return nil
}
```

**Complexity Analysis:**
- Time Complexity: O(n)
  - Single pass through the array
- Space Complexity: O(n)
  - Hash map can store up to n elements

## Solution Comparison Table

| Approach | Time Complexity | Space Complexity | Advantages | Disadvantages |
|----------|----------------|------------------|------------|---------------|
| Brute Force | O(n²) | O(1) | Simple to implement, No extra space | Slow for large inputs |
| Hash Map | O(n) | O(n) | Fast, Single pass solution | Uses extra space |

## Follow-up Questions
1. Can you solve it in O(n) time complexity?
2. Can you solve it with constant space complexity?
3. What if the array is sorted?

## Related Problems
- Three Sum
- Four Sum
- Two Sum II - Input Array Is Sorted
- Two Sum Less Than K
