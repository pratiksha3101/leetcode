# Container With Most Water

## Problem Description

[LeetCode Problem 11 - Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

### Problem Statement

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `i`-th line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

**Return the maximum amount of water a container can store.**

**Note:** You may not slant the container.

### Example

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. 
In this case, the max area of water (blue section) the container can contain is 49.
```

## Solution Approaches

### 1. Brute Force Approach

#### Complexity Analysis
- **Time Complexity**: O(n²)
- **Space Complexity**: O(1)

#### Algorithm
- Use nested loops to check every possible pair of lines
- Calculate the area for each pair
- Keep track of the maximum area found

```go
func bruteForce(height []int) int {
    maxArea := 0

    for i := 0; i < len(height); i++ {
        for j := i+1; j < len(height); j++ {
            w := j-i
            h := min(height[i], height[j])
            currentArea := w * h
            maxArea = max(maxArea, currentArea)
        }
    }

    return maxArea
}
```

### 2. Optimal Two-Pointer Approach

#### Complexity Analysis
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)

#### Algorithm
- Start with the widest container (first and last lines)
- Move the pointer with the shorter line inward
- Calculate and update the maximum area
- Repeat until pointers meet

```go
func optimal(height []int) int {
    maxArea := 0
    left, right := 0, len(height)-1

    for left < right {
        currentArea := (right - left) * min(height[right], height[left])
        maxArea = max(maxArea, currentArea)

        if height[left] < height[right] {
            left++
        } else {
            right--
        }
    }

    return maxArea
}
```

### Main Function

```go
func maxArea(height []int) int {
    // Uncomment the approach you want to use
    // return bruteForce(height)
    return optimal(height)
}
```

## Key Insights

1. The area is calculated by the width (distance between lines) multiplied by the height of the shorter line.
2. The two-pointer approach is more efficient as it eliminates unnecessary calculations.
3. By moving the pointer with the shorter line, we ensure we don't miss a potentially larger area.

## Leetcode Submission Details

- **Acceptance Rate**: Around 55.5%
- **Difficulty**: Medium

## Tips for Solving

- Always consider the constraints of the problem
- Think about how to reduce unnecessary computations
- Practice visualizing the problem (draw it out if needed)
