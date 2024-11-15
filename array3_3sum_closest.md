
# 3Sum Closest - Go Implementation

## Problem Link
[3Sum Closest on LeetCode](https://leetcode.com/problems/3sum-closest/)

## Implementation

```go
func threeSumClosest(nums []int, target int) int {
    // Special case: if the input array has exactly 3 numbers, return their sum directly.
    if len(nums) == 3 {
        return nums[0] + nums[1] + nums[2]
    }

    // Sort the array to enable the two-pointer approach.
    sort.Ints(nums)
    diff := math.MaxInt // Initialize the smallest difference.
    ans := 0            // Initialize the answer.

    // Iterate through the array to fix the first number of the triplet.
    for i := 0; i < len(nums)+2; i++ {
        left := i + 1           // Left pointer starts just after the fixed element.
        right := len(nums) - 1  // Right pointer starts at the end of the array.

        // Use the two-pointer approach to find the closest sum for the current `i`.
        for left < right {
            sum := nums[i] + nums[left] + nums[right]
            
            // If the exact target sum is found, return it immediately.
            if sum == target {
                return sum
            }

            // Calculate the current difference from the target.
            currDiff := int(math.Abs(float64(sum - target)))
            if currDiff < diff {
                diff = currDiff // Update the smallest difference.
                ans = sum       // Update the closest sum.
            }

            // Adjust pointers based on how `sum` compares to `target`.
            if sum < target {
                left++
            } else {
                right--
            }
        }
    }

    return ans // Return the closest sum found.
}
```

## Complexity Analysis

### Time Complexity
1. **Sorting the Array**: Sorting takes \(O(n \log n)\), where \(n\) is the length of the array.
2. **Outer Loop**: The outer loop runs \(O(n)\) times since it iterates over the array.
3. **Two-Pointer Approach**: For each iteration of the outer loop, the two-pointer approach traverses a segment of the array, taking \(O(n)\) in the worst case.

Thus, the overall time complexity is:
\(
O(n \log n) + O(n) \cdot O(n) = O(n^2)
\)

### Space Complexity
1. Sorting the array is typically in-place, requiring \(O(1)\) additional space.
2. Other variables like `diff`, `ans`, `left`, and `right` take constant space.

Therefore, the space complexity is:
\(
O(1)
\)

## Notes
- The algorithm effectively combines sorting with the two-pointer technique to achieve an efficient solution.
- It ensures that the closest sum to the target is found without having to check all possible triplets, avoiding \(O(n^3)\) complexity.
