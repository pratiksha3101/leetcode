# Majority Element

## Problem Description

This is a solution to the LeetCode problem [Majority Element](https://leetcode.com/problems/majority-element/).

The goal is to find the majority element in an array. A majority element is an element that appears more than ⌊n / 2⌋ times in the array, where n is the array's length. It is guaranteed that a majority element always exists in the input array.

## Solution Approaches

### 1. Brute Force Approach
- **Method**: `brute()`
- **Time Complexity**: O(n)
- **Space Complexity**: O(n)
- **Approach**: 
  - Use a hash map to count element frequencies
  - Return element when its count exceeds n/2

### 2. Sorting-Based Approach
- **Method**: `optimizeSortingBased()`
- **Time Complexity**: O(n log n)
- **Space Complexity**: O(1)
- **Approach**:
  - Sort the array
  - Count consecutive occurrences
  - Return element with count > n/2

### 3. Moore's Voting Algorithm
- **Method**: `mooresVotingAlgo()`
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)
- **Approach**:
  - Use a candidate and count tracking
  - Cancel out different elements
  - The remaining candidate is the majority element

## Complete Solution Code

```go
func majorityElement(nums []int) int {
    return mooresVotingAlgo(nums)
}

// Moore's voting algorithm
// Time Complexity: O(n)
// Space Complexity: O(1)
func mooresVotingAlgo(nums []int) int {
    candidate := 0
    count := 0

    for i := 0; i < len(nums); i++ {
        if count == 0 {
            candidate = nums[i]
        }

        if candidate == nums[i] {
            count++
        } else {
            count--
        }
    }

    return candidate
}
```

## Complexity Analysis

| Approach | Time Complexity | Space Complexity | Pros | Cons |
|----------|-----------------|------------------|------|------|
| Hash Map | O(n) | O(n) | Simple to understand | Uses extra space |
| Sorting | O(n log n) | O(1) | In-place solution | Modifies input array |
| Moore's Voting | O(n) | O(1) | Most efficient | Requires understanding of the algorithm |

## Moore's Voting Algorithm Explained

The algorithm works on the principle of cancellation:
1. If an element appears more than n/2 times, it will always remain after cancelling out other elements
2. Start with a candidate and a count
3. If count becomes 0, choose a new candidate
4. Increment count for matching elements
5. Decrement count for different elements

## Example

```go
nums := []int{3,2,3}
result := majorityElement(nums)
// result is 3

nums := []int{2,2,1,1,1,2,2}
result := majorityElement(nums)
// result is 2
```

## Notes
- Guaranteed that a majority element exists
- O(1) space solutions are preferred
- Moore's Voting Algorithm is the most optimal approach

## Potential Follow-up Questions
- How would you verify the majority element?
- What if the majority element might not exist?
- Can you solve this with different constraints?
