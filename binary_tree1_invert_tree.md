# Invert Binary Tree

## Problem Link
[LeetCode - 226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

## Problem Description
Given the root of a binary tree, invert the tree, and return its root.

## Examples

### Example 1:
```
Input:
     4
   /   \
  2     7
 / \   / \
1   3 6   9

Output:
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

## Solution Approach in Go

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func invertTree(root *TreeNode) *TreeNode {
    traverse(root)
    return root
}

func traverse(root *TreeNode) {
    if root == nil {
        return 
    }

    temp := root.Left
    root.Left = root.Right
    root.Right = temp

    traverse(root.Left)
    traverse(root.Right)
}
```

## Solution Explanation
1. The solution uses a recursive approach to invert the binary tree
2. For each node:
   - We store the left child in a temporary variable
   - Swap the left and right children
   - Recursively invert the left and right subtrees
3. The base case is when we reach a null node (leaf node's children)
4. The recursion follows a pre-order traversal pattern (process node, then left child, then right child)

## Complexity Analysis

### Time Complexity: O(n)
- Where n is the number of nodes in the binary tree
- We visit each node exactly once during the recursion
- At each node, we perform O(1) operations (swapping pointers)

### Space Complexity: O(h)
- Where h is the height of the tree
- This space is used by the recursion stack
- In the worst case (skewed tree), h = n, making it O(n)
- In the best case (balanced tree), h = log(n), making it O(log n)

## Edge Cases
1. Empty tree (root = nil) → Returns nil
2. Single node tree → Returns the same node
3. Complete binary tree → All levels are inverted
4. Skewed tree → Becomes skewed in opposite direction

## Insertion Point for Your Image![Screenshot from 2024-11-20 12-49-52](https://github.com/user-attachments/assets/159619ae-224c-47b5-a021-19b44735719e)


## Alternative Approaches
1. **Iterative using Queue (BFS)**
   - Use a queue to process nodes level by level
   - Space complexity: O(w) where w is max width of tree

2. **Iterative using Stack (DFS)**
   - Similar to recursive but using explicit stack
   - Space complexity: O(h) where h is height of tree

## Common Pitfalls
1. Forgetting to handle null nodes
2. Not properly storing the left child before overwriting
3. Recursing on original children instead of swapped children

## Follow-up Questions
1. How would you modify this to work iteratively?
2. Can you do this in-place without using extra space?
3. How would you handle a general n-ary tree inversion?
