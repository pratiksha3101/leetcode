# Find Missing and Repeated Values

## Problem Description

This is a solution to the LeetCode problem [Find Missing and Repeated Values](https://leetcode.com/problems/find-missing-and-repeated-values/).

### Problem Statement
Given a 0-indexed 2D integer matrix `grid`, there will be a repeated integer and a missing integer:
- A repeated integer appears two times in the grid
- A missing integer is an integer in the range `[1, n²]` that does not appear in the grid

The task is to find and return the repeated and missing integers `[repeated, missing]`.

## Solution Approaches

### 1. Optimal Approach 
- **Method**: `optimal()`
- **Time Complexity**: O(n²)
- **Space Complexity**: O(n²)
- **Key Steps**:
  1. Use a map to track unique elements
  2. Find repeated element during first pass
  3. Calculate expected sum of all elements
  4. Compute missing element using mathematical formula

## Complete Solution Code

```go
func findMissingAndRepeatedValues(grid [][]int) []int {
    return optimal(grid)
}

func optimal(grid [][]int) []int {
    a, b, actualSum := 0, 0, 0

    n := len(grid)
    mp := make(map[int]struct{})

    for i := 0; i < n; i++ {
        for j := 0; j < len(grid[i]); j++ {
            actualSum += grid[i][j]
            if _, exists := mp[grid[i][j]]; exists {
                a = grid[i][j]
            } else {
                mp[grid[i][j]] = struct{}{}
            }
        }
    }

    expectedSum := (n*n) * (n*n + 1) / 2
    b = expectedSum + a - actualSum
    return []int{a,b}
}
```

## Time Complexity Analysis: O(n²)

1. **Outer Loop (`for i := 0; i < n; i++`)**:
   * Iterates over each row in the grid
   * Total iterations: O(n)

2. **Inner Loop (`for j := 0; j < len(grid[i]); j++`)**:
   * Iterates over each column in the current row
   * Since the grid is n×n, the total number of elements in the grid is n²
   * Total iterations: O(n²)

3. **Map Operations (`mp[grid[i][j]]` and `mp[grid[i][j]] = struct{}{}`)**:
   * Lookup and insertion in a map are O(1) on average
   * These operations occur once for each element in the grid
   * Total cost for map operations: O(n²)

4. **Calculation of `expectedSum`**:
   * Computing the formula (n×n) × ((n×n)+1)/2 is O(1)

**Overall Time Complexity**: O(n²)

## Space Complexity Analysis: O(n²)

1. **Map `mp`**:
   * Stores each unique number in the grid, up to n² elements in the worst case
   * Space complexity of the map: O(n²)

2. **Auxiliary Variables (`a`, `b`, `actualSum`, `expectedSum`)**:
   * Fixed number of variables: O(1)

3. **Result Array (`[]int{a, b}`)**:
   * Constant size: O(1)

**Overall Space Complexity**: O(n²)

## Example

```go
grid := [][]int{{1,3},{2,2}}
result := findMissingAndRepeatedValues(grid)
// result is [2, 4]
// 2 is repeated, 4 is missing
```

## Key Insights
- Uses mathematical formula to compute missing element
- Efficiently tracks unique and repeated elements
- Handles n×n grid constraints
- Single pass solution

## Potential Follow-up Questions
- Can you solve this with O(1) space?
- How would you modify for different grid sizes?
- What if the grid is not guaranteed to be n×n?

## Notes
- Works for 1-indexed value range
- Assumes grid is n×n square matrix
- Guaranteed to have exactly one repeated and one missing value
