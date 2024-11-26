# Valid Anagram - LeetCode Problem 242

## Problem Link
[LeetCode - Valid Anagram](https://leetcode.com/problems/valid-anagram/)

## Problem Description
An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once. For example, "listen" and "silent" are anagrams.

## Solution in Go

```go
func isAnagram(s string, t string) bool {
    if len(s) != len(t) {
        return false
    }

    mp := make(map[rune]int)
    for _, c := range s {
        mp[c]++
    }

    for _, c := range t {
        count, exists := mp[c]
        if !exists || count < 1 {
            return false
        }

        mp[c]--
    }

    return true
}
```

## Complexity Analysis

### Time Complexity: O(n)
- First loop iterating through `s`: O(n)
- Second loop iterating through `t`: O(n)
- Map operations (insert, lookup, decrement): O(1)
- Total time complexity: O(n)

### Space Complexity: O(k)
- Where k is the number of unique characters
- In the worst case (all unique characters), k could be as large as the input string length
- Typically bounded by the character set size (26 for lowercase English letters)

## Approach Explanation
1. First, check if the lengths of both strings are equal
2. Create a frequency map of characters in the first string
3. Iterate through the second string:
   - Check if each character exists in the map
   - Decrement its count
   - Return false if character not found or count becomes negative
4. Return true if all characters are matched

## Example

```
Input: s = "anagram", t = "nagaram"
Output: true

Input: s = "rat", t = "car"
Output: false
```

## Alternative Solutions
1. Sorting approach (less efficient)
2. Fixed-size array counting for known character sets
3. Using XOR bit manipulation

## Edge Cases to Consider
- Empty strings
- Strings with different lengths
- Strings with Unicode characters
- Case sensitivity

### Note: This solution, using rune in Go is actually perfect for handling Unicode characters. A rune represents a Unicode code point, which means the solution can work with characters beyond just ASCII.
