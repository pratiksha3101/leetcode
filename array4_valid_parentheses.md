# Valid Parentheses 

## Problem Link
[LeetCode - Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

## Problem Statement
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

## Complexity
- Time Complexity: `O(n)` - where n is the length of the string
- Space Complexity: `O(n)` - in worst case, stack stores n/2 characters

## Solution

```go
func isValid(s string) bool {
    if len(s) == 0 || len(s)%2 != 0 {
        return false
    }
    
    stack := []rune{}
    for _, p := range s {  
        if p == '(' || p == '{' || p == '[' {
            stack = append(stack, p)
        }

        if p == ')' || p == '}' || p == ']' {
            if len(stack) == 0 {
                return false
            }
            lastElement := stack[len(stack)-1]
            if p == ')' && lastElement != '(' ||
               p == '}' && lastElement != '{' ||
               p == ']' && lastElement != '[' {
                return false
            }
            stack = stack[:len(stack)-1] 
        }
    }

    return len(stack) == 0
}
```

## Understanding the Stack Data Structure

### What is a Stack?
A stack is a linear data structure that follows the Last-In-First-Out (LIFO) principle. Think of it like a stack of plates - you can only add or remove plates from the top.

### Key Operations
1. **Push**: Add an element to the top of the stack
2. **Pop**: Remove the topmost element from the stack
3. **Peek/Top**: View the topmost element without removing it

### Visual Representation
```
Push operations:        Pop operations:
[a] ← Top              [c] ← Remove this
[b]                    [b]
[c]                    [a]
```

### Why Stack for Parentheses Matching?
A stack is perfect for this problem because:
1. When we see an opening bracket, we push it onto the stack
2. When we see a closing bracket, we check if it matches with the most recent opening bracket (top of stack)
3. The LIFO nature ensures brackets are closed in the correct order

## Solution Explanation

1. **Early Validation**:
   ```go
   if len(s) == 0 || len(s)%2 != 0 {
       return false
   }
   ```
   - Empty string is invalid
   - String with odd length can't have matching pairs

2. **Stack Implementation**:
   ```go
   stack := []rune{}
   ```
   - Using a slice as a stack
   - `rune` type to handle individual characters

3. **Processing Characters**:
   ```go
   for _, p := range s {
       if p == '(' || p == '{' || p == '[' {
           stack = append(stack, p)
       }
   ```
   - Push all opening brackets onto stack

4. **Matching Brackets**:
   ```go
   if p == ')' || p == '}' || p == ']' {
       if len(stack) == 0 {
           return false
       }
       lastElement := stack[len(stack)-1]
       if p == ')' && lastElement != '(' ||
          p == '}' && lastElement != '{' ||
          p == ']' && lastElement != '[' {
           return false
       }
       stack = stack[:len(stack)-1]
   }
   ```
   - For closing brackets:
     - Check if stack is empty (no matching open bracket)
     - Check if top of stack matches
     - Pop the matching bracket

5. **Final Validation**:
   ```go
   return len(stack) == 0
   ```
   - Stack should be empty if all brackets were matched

## Example
Input: `"({[]})"` 
```
Step 1: Push '('    Stack: ['(']
Step 2: Push '{'    Stack: ['(', '{']
Step 3: Push '['    Stack: ['(', '{', '[']
Step 4: Pop '['     Stack: ['(', '{']     (matches ']')
Step 5: Pop '{'     Stack: ['(']          (matches '}')
Step 6: Pop '('     Stack: []             (matches ')')
Result: Valid (empty stack)
```
