# Single Number

## Problem Description

This is a solution to the LeetCode problem [Single Number](https://leetcode.com/problems/single-number/).

### Problem Statement
Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one.

## Solution

```go
func singleNumber(nums []int) int {
    res := 0

    for _, n := range nums {
        res = res ^ n
    }

    return res
}
```

## XOR (Exclusive OR) Operation: Deep Dive

### What is XOR?
XOR is a bitwise operation with unique properties that make it incredibly useful in solving certain programming problems.

### XOR Truth Table
| A | B | A XOR B |
|---|---|---------|
| 0 | 0 |    0    |
| 0 | 1 |    1    |
| 1 | 0 |    1    |
| 1 | 1 |    0    |

### Key Properties of XOR

1. **Commutative Property**
   ```
   a ^ b = b ^ a
   ```

2. **Associative Property**
   ```
   (a ^ b) ^ c = a ^ (b ^ c)
   ```

3. **Identity Element**
   ```
   a ^ 0 = a
   ```

4. **Self-Cancellation**
   ```
   a ^ a = 0
   ```

### Why XOR Works for Single Number Problem

Consider an array: `[4, 1, 2, 1, 2]`

XOR Operation Steps:
1. Start with `res = 0`
2. `0 ^ 4 = 4`
3. `4 ^ 1 = 5`
4. `5 ^ 2 = 7`
5. `7 ^ 1 = 6`
6. `6 ^ 2 = 4`

The single number emerges because:
- Duplicate numbers cancel each other out
- The unique number remains

### Complexity Analysis

- **Time Complexity**: O(n)
  * Single pass through the array
  * Constant-time XOR operation

- **Space Complexity**: O(1)
  * Only one variable used
  * No additional data structures

## Example

```go
nums := []int{4, 1, 2, 1, 2}
result := singleNumber(nums)
// result is 4
```

## Real-world XOR Applications

1. **Cryptography**
   - Encryption and decryption algorithms
   - Generating random numbers

2. **Error Detection**
   - Checksum calculations
   - Parity bit computation

3. **Low-Level Programming**
   - Bit manipulation
   - Efficient swapping without temporary variables

## Limitations and Considerations

- Works only when every element appears twice
- Assumes one unique element
- Requires array to meet specific conditions

## Advanced XOR Techniques

1. **Swapping without Temporary Variable**
   ```go
   a = a ^ b
   b = a ^ b
   a = a ^ b
   ```

2. **Finding Missing Number**
   ```go
   missing = (1 ^ 2 ^ ... ^ n) ^ (array elements)
   ```

## Potential Follow-up Questions

- What if multiple elements appear an odd number of times?
- How to handle different array constraints?
- Can you solve this with different time/space complexity?

## Notes

- Elegant and efficient solution
- Leverages bitwise operation properties
- Constant space complexity
- Single pass solution
