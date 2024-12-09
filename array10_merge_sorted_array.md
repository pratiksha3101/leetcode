# Merge Sorted Array

## Problem Description

This is a solution to the LeetCode problem [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/).

The goal is to merge two sorted integer arrays `nums1` and `nums2` into a single sorted array. `nums1` has a length of `m + n`, where the first `m` elements are the initial elements to be merged, and the last `n` elements are set to 0 and should be used to place the merged elements.

## Solution

```go
func merge(nums1 []int, m int, nums2 []int, n int)  {
    // Uncomment the approach you want to use
    // withExtraSpace(nums1, nums2, m, n)
    withoutExtraSpace(nums1, nums2, m, n)
}

// Time Complexity: O(m+n)
// Space Complexity: O(m+n)
func withExtraSpace(nums1, nums2 []int, m, n int) {
    p1 := 0
    p2 := 0

    res := []int{} // The size of res is (m+n)
    for p1 < m && p2 < n {
        if nums1[p1] < nums2[p2] {
            res = append(res, nums1[p1])
            p1++
        } else {
            res = append(res, nums2[p2])
            p2++
        }
    }

    for p1 < m {
        res = append(res, nums1[p1])
        p1++
    }
    
    // Add remaining elements from nums2 if any
    for p2 < n {
        res = append(res, nums2[p2])
        p2++
    }

    copy(nums1,res)    
}

// Time Complexity: O(m+n)
// Space Complexity: O(1)
func withoutExtraSpace(nums1, nums2 []int, m, n int) {
    p := m + n - 1
    i := m - 1
    j := n - 1

    for i >= 0 && j >= 0 {
        if nums1[i] > nums2[j] {
            nums1[p] = nums1[i]
            i--
        } else {
            nums1[p] = nums2[j]
            j--
        }

        p--
    }

    // Handle remaining elements from nums2
    for j >= 0 {
        nums1[p] = nums2[j]
        j--
        p--
    }
}
```

## Approaches

### 1. With Extra Space Approach
- **Method**: `withExtraSpace()`
- **Time Complexity**: O(m+n)
- **Space Complexity**: O(m+n)
- **Approach**: 
  - Create a new result array
  - Compare and merge elements from both input arrays
  - Copy the merged result back to `nums1`

### 2. Without Extra Space Approach
- **Method**: `withoutExtraSpace()`
- **Time Complexity**: O(m+n)
- **Space Complexity**: O(1)
- **Approach**:
  - Start from the end of both arrays
  - Compare and place elements from the back of `nums1`
  - Handle remaining elements from `nums2` if any

## Key Features

- Handles merging of two sorted arrays in-place
- Supports two different implementation strategies
- Efficient time complexity for both approaches
- Minimal space usage in the optimized version

## Example

```go
nums1 := []int{1,2,3,0,0,0}
m := 3
nums2 := []int{2,5,6}
n := 3

merge(nums1, m, nums2, n)
// nums1 is now [1,2,2,3,5,6]
```

## Complexity Analysis

| Approach | Time Complexity | Space Complexity | Pros | Cons |
|----------|-----------------|------------------|------|------|
| Extra Space | O(m+n) | O(m+n) | Simple to implement | Uses additional memory |
| In-place | O(m+n) | O(1) | Memory efficient | Slightly more complex logic |

## Notes
- Ensure `nums1` has enough space to accommodate elements from `nums2`
- The solution works with sorted input arrays
- Modifies `nums1` in-place
