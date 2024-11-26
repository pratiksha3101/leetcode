# Binary Search Algorithm

## Problem Statement
[Binary Search - LeetCode](https://leetcode.com/problems/binary-search/)

The problem requires implementing an efficient search algorithm to find a target value in a sorted array. The algorithm should return the index of the target if found, or -1 if the target is not present.

## Algorithm Explanation

Binary search is an efficient algorithm for searching a sorted array by repeatedly dividing the search interval in half. It works on the principle of eliminating half of the remaining elements at each step.

### Key Principles
- The array must be sorted in ascending order
- Uses a divide-and-conquer approach
- Dramatically reduces search space in each iteration

### Implementation in Go

```go
func search(nums []int, target int) int {
    left, right := 0, len(nums) - 1

    for left <= right {
        mid := left + (right - left)/2  // Correct mid-point calculation

        if nums[mid] == target {
            return mid
        } else if target < nums[mid] {
            right = mid - 1
        } else {
            left = mid + 1
        }
    }

    return -1    
}
```

## Be Careful: Mid-Point Calculation

### Preventing Integer Overflow
The expression `mid := left + (right - left)/2` is crucial for preventing integer overflow. 

#### Why is this important?
- In some languages, directly calculating `(left + right)/2` can cause integer overflow
- When `left` and `right` are large integers, their sum might exceed the maximum integer value
- The alternative calculation `left + (right - left)/2` mathematically equivalent but safer

#### Comparison of Approaches
1. Unsafe approach: `mid = (left + right) / 2`
   - Risk of integer overflow
   - Potential to cause unexpected behavior in large arrays

2. Safe approach: `mid = left + (right - left) / 2`
   - Prevents integer overflow
   - Works correctly for very large arrays
   - Mathematically equivalent to the first approach

### Algorithm Steps
1. Initialize two pointers: `left` at the start and `right` at the end of the array
2. Calculate the middle index `mid` safely
3. Compare the middle element with the target:
   - If equal, return the middle index
   - If target is less, search the left half
   - If target is greater, search the right half
4. Repeat until the target is found or search space is exhausted

## Complexity Analysis

### Time Complexity: O(log n)
- Each iteration reduces the search space by half
- Logarithmic time complexity makes it extremely efficient for large sorted arrays
- Best and worst-case scenarios both have O(log n) time complexity

### Space Complexity: O(1)
- Uses constant extra space
- In-place algorithm with only a few variables regardless of input size

## Common Pitfalls
- Ensure the input array is sorted before applying binary search
- Be careful with integer overflow when calculating `mid`
- Handle edge cases like empty arrays or single-element arrays

## Variations
- Recursive implementation
- Finding the first or last occurrence of a target
- Searching in rotated sorted arrays

## When to Use
- Searching in large sorted arrays
- Scenarios requiring quick lookups
- When the dataset is static and sorted
