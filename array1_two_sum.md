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

  [Previous content remains the same...]

## Follow-up Questions & Solutions

### 1. Can you solve it in O(n) time complexity?
**Answer**: Yes, using the Hash Map approach already demonstrates an O(n) time complexity solution.
```go
func twoSumHashMap(nums []int, target int) []int {
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

### 2. Can you solve it with constant space complexity?
**Answer**: Yes, but with some trade-offs:
1. If we're allowed to modify the input array:
```go
func twoSumConstantSpace(nums []int, target int) []int {
    // Create array of indices
    indices := make([]int, len(nums))
    for i := range indices {
        indices[i] = i
    }
    
    // Sort nums and keep track of original indices
    sort.Slice(indices, func(i, j int) bool {
        return nums[indices[i]] < nums[indices[j]]
    })
    
    // Use two pointers approach
    left, right := 0, len(nums)-1
    for left < right {
        sum := nums[indices[left]] + nums[indices[right]]
        if sum == target {
            return []int{indices[left], indices[right]}
        }
        if sum < target {
            left++
        } else {
            right--
        }
    }
    return nil
}
```
Time Complexity: O(n log n) due to sorting
Space Complexity: O(1) if we modify input array, O(n) if we need to preserve original array

### 3. What if the array is sorted?
**Answer**: If the array is already sorted, we can use the Two Pointers approach, which is more efficient:
```go
func twoSumSorted(nums []int, target int) []int {
    left, right := 0, len(nums)-1
    
    for left < right {
        sum := nums[left] + nums[right]
        if sum == target {
            return []int{left, right}
        }
        if sum < target {
            left++
        } else {
            right--
        }
    }
    return nil
}
```
**Complexity Analysis for Sorted Array:**
- Time Complexity: O(n)
- Space Complexity: O(1)

### Summary Table of All Approaches

| Approach | Time Complexity | Space Complexity | Requirements |
|----------|----------------|------------------|--------------|
| Brute Force | O(n²) | O(1) | None |
| Hash Map | O(n) | O(n) | None |
| Two Pointers | O(n log n) | O(1) | Needs sorting |
| Two Pointers (Sorted) | O(n) | O(1) | Array must be pre-sorted |

### Key Takeaways
1. The Hash Map solution provides the best balance of time and space complexity for unsorted arrays
2. If memory is a constraint and the array is sorted (or can be sorted), the Two Pointers approach is optimal
3. For already sorted arrays, Two Pointers approach is the best choice as it achieves O(n) time with O(1) space
4. The Brute Force approach, while simple, is generally not recommended due to its O(n²) time complexity

### Trade-offs to Consider
1. **Hash Map Approach**
   - Pros: Single pass, O(n) time
   - Cons: Uses extra space
   
2. **Two Pointers (Sorted)**
   - Pros: O(1) space, simple implementation
   - Cons: Requires sorted array, sorting adds O(n log n) if array isn't sorted

3. **Brute Force**
   - Pros: Simple to implement, no extra space
   - Cons: Very slow for large inputs
