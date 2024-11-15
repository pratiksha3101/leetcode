# Three Sum Problem

[LeetCode Problem Link](https://leetcode.com/problems/3sum/)

## Problem Description
Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

## Solutions

### 1. Brute Force Approach
This solution checks all possible triplet combinations using three nested loops.

```go
func bruteForce(nums []int) [][]int {
    result := [][]int{}
    seen := make(map[string]bool)

    for i := 0; i < len(nums); i++ {
        for j := i+1; j < len(nums); j++ {
            for k := j+1; k < len(nums); k++ {
                if nums[i] + nums[j] + nums[k] == 0 && i != j && i !=k && j!= k {
                    triplet := []int{nums[i], nums[j], nums[k]}
                    sort.Ints(triplet)

                    key := fmt.Sprintf("%d,%d,%d", triplet[0], triplet[1], triplet[2])

                    if !seen[key] {
                        result = append(result, []int{triplet[0], triplet[1], triplet[2]})
                        seen[key] = true
                    }
                }
            }
        }
    }
    return result
}
```

**Complexity Analysis:**
- Time Complexity: O(n³) due to three nested loops
- Space Complexity: O(n²) for storing unique triplets in the map

### 2. Two Pointers Approach
This solution improves efficiency by sorting the array first and using two pointers.

```go
func twoPointers(nums []int) [][]int {
    sort.Ints(nums)
    res := [][]int{}
    uniqueTriplets := make(map[string]bool)

    for i := 0; i < len(nums) - 2; i++ {
        left := i + 1
        right := len(nums) - 1

        for left < right {
            sum := nums[i] + nums[left] + nums[right] 
            
            if sum == 0 {
                triplet := []int{nums[i], nums[left], nums[right]}  

                key := fmt.Sprintf("%d,%d,%d", nums[i], nums[left], nums[right])
                if !uniqueTriplets[key] {
                    res = append(res, triplet)
                    uniqueTriplets[key] = true
                }

                left++
                right--           
            } else if sum < 0 {
                left++
            } else {
                right--
            }
        }
    }
    return res
}
```

**Complexity Analysis:**
- Time Complexity: O(n²)
  - Sorting: O(n log n)
  - Two nested loops: O(n²)
  - Overall: O(n log n + n²) = O(n²)
- Space Complexity: O(n)
  - For storing unique triplets and result

### 3. Optimized Two Pointers Approach
This solution further optimizes by handling duplicates without using a hash map.

```go
func twoPointersOptimized(nums []int) [][]int {
    var res [][]int
    if len(nums) < 3 {
        return res
    }

    sort.Ints(nums)

    for i := 0; i < len(nums)-2; i++ {
        // Skip duplicates for first number
        if i > 0 && nums[i] == nums[i-1] {
            continue
        }

        left, right := i+1, len(nums)-1

        for left < right {
            target := nums[i] + nums[left] + nums[right]

            if target == 0 {
                res = append(res, []int{nums[i], nums[left], nums[right]})
                left++
                right--    

                // Skip duplicates for second number
                for left < right && nums[left] == nums[left-1] {
                    left++
                }
                // Skip duplicates for third number
                for left < right && nums[right] == nums[right+1] {
                    right--
                }
            } else if target > 0 {
                right--
            } else {
                left++
            }
        }
    }
    return res
}
```

**Complexity Analysis:**
- Time Complexity: O(n²)
  - Same as the previous approach
- Space Complexity: O(1)
  - No extra space used except for output array
  - Improves on previous approach by eliminating hash map

## Key Optimizations in Final Solution
1. **Early Exit**: Returns empty result if array length < 3
2. **Efficient Duplicate Handling**:
   - Skips duplicate values for the first number
   - Skips duplicate values for second and third numbers after finding a valid triplet
3. **No Hash Map**: Uses sorted array properties to handle duplicates instead of hash map
4. **Two Pointers**: Uses two-pointer technique to reduce time complexity from O(n³) to O(n²)

## Example Walkthrough
```
Input: nums = [-1,0,1,2,-1,-4]
Sorted array: [-4,-1,-1,0,1,2]

1. First iteration (i=0, -4):
   - Look for pairs that sum to 4
   
2. Second iteration (i=1, -1):
   - Find pairs that sum to 1
   - Find [-1,0,1]
   
3. Skip next -1 as it's duplicate
   
4. Continue with remaining elements...

Output: [[-1,-1,2],[-1,0,1]]
```
