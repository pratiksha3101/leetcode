# Merge Two Sorted Lists

## Problem Link
[LeetCode - Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

## Problem Statement
You are given the heads of two sorted linked lists `list1` and `list2`. Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists. Return the head of the merged linked list.

## Complexity
- Time Complexity: `O(n + m)` where n and m are the lengths of the two lists
- Space Complexity: `O(1)` as only constant extra space is used

## Solution

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func mergeTwoLists(list1 *ListNode, list2 *ListNode) *ListNode {
    dummy := &ListNode{}
    current := dummy

    for list1 != nil && list2 != nil {
        if list1.Val < list2.Val {
            current.Next = list1
            list1 = list1.Next
        } else {
            current.Next = list2
            list2 = list2.Next
        }

        current = current.Next
    }   

    // attach the remaining nodes if exists
    if list1 != nil {
        current.Next = list1
    } else if list2 != nil {
        current.Next = list2
    }

    return dummy.Next
}
```

## Understanding Linked Lists

### What is a Linked List?
A linked list is a linear data structure where elements (nodes) are connected using pointers. Each node contains:
1. Data (Val in this case)
2. Reference to the next node (Next pointer)

### Visual Representation
```
List Structure:
[1] -> [3] -> [4]
 ↑     ↑     ↑
Val   Next   Next
```

## Solution Explanation

1. **Initialize Pointers**:
   ```go
   dummy := &ListNode{}
   current := dummy
   ```
   - Create a dummy node to handle edge cases
   - Use current pointer to track where to add next node

2. **Main Merging Process**:
   ```go
   for list1 != nil && list2 != nil {
       if list1.Val < list2.Val {
           current.Next = list1
           list1 = list1.Next
       } else {
           current.Next = list2
           list2 = list2.Next
       }
       current = current.Next
   }
   ```
   - Compare values from both lists
   - Attach smaller value node to result
   - Move pointer in the list we took from
   - Move current pointer forward

3. **Handle Remaining Nodes**:
   ```go
   if list1 != nil {
       current.Next = list1
   } else if list2 != nil {
       current.Next = list2
   }
   ```
   - Attach any remaining nodes from either list
   - This works because input lists are already sorted

4. **Return Result**:
   ```go
   return dummy.Next
   ```
   - Skip the dummy node and return actual head

## Example Walkthrough

Input:
```
list1: 1 -> 3 -> 4
list2: 2 -> 4 -> 6
```

Merging Process:
```
Step 1: 
dummy -> 1 -> ...  (1 < 2)
list1: 3 -> 4
list2: 2 -> 4 -> 6

Step 2:
dummy -> 1 -> 2 -> ...  (3 > 2)
list1: 3 -> 4
list2: 4 -> 6

Step 3:
dummy -> 1 -> 2 -> 3 -> ...  (3 < 4)
list1: 4
list2: 4 -> 6

... and so on
```

Final Output:
```
1 -> 2 -> 3 -> 4 -> 4 -> 6
```

## Key Points
1. Solution maintains constant space complexity by reusing existing nodes
2. Dummy node simplifies edge cases (empty lists, inserting at head)
3. Time complexity is linear as we process each node exactly once
4. Input lists must be pre-sorted for correct results

## Common Edge Cases
1. Empty list(s): `list1 = nil` and/or `list2 = nil`
2. Lists of different lengths
3. Lists with duplicate values
4. Single node lists

This solution handles all these cases correctly through:
- Initial dummy node
- Null checks in the loop condition
- Remaining nodes handling
