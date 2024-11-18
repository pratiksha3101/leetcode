# Valid Palindrome

## Problem
[LeetCode Problem Link](https://leetcode.com/problems/valid-palindrome/)

## Solution (Go)

```go
// Time Complexity: O(n)
// Space Complexity: O(1)
func isPalindrome(s string) bool {
    left, right := 0, len(s) - 1

    for left < right {
        for left < right && !isAlphanumeric(string(s[left])) {
            left++        
        }

        for left < right && !isAlphanumeric(string(s[right])) {
            right--        
        }

        if strings.ToLower(string(s[left])) != strings.ToLower(string(s[right])) {
            return false
        }

        left++
        right--
    }

    return true
}

func isAlphanumeric(s string) bool {
    if ((s >= "A" && s <= "Z") || (s >= "a" && s <= "z")) || (s >= "0" && s <= "9") {
        return true 
    }

    return false
}
```

## Approach
- Use two-pointer technique (left and right pointers)
- Skip non-alphanumeric characters
- Compare characters case-insensitively
- Return false if characters don't match
- Return true if entire string is traversed

## Complexity
- **Time Complexity**: O(n), where n is the length of the string
- **Space Complexity**: O(1), using only two pointers

## Example
```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: After removing non-alphanumeric characters, it reads "amanaplanacanalpanama"
```
