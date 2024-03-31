# binary-trees-dfs
## binary-trees-dfs-01
111. Minimum Depth of Binary Tree
https://leetcode.com/problems/minimum-depth-of-binary-tree/editorial/
Given a binary tree, find its minimum depth.
The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.
Note: A leaf is a node with no children.
Example 1:
Input: root = [3,9,20,null,null,15,7]
Output: 2
Example 2:
Input: root = [2,null,3,null,4,null,5,null,6]
Output: 5

Constraints:
The number of nodes in the tree is in the range [0, 105].
-1000 <= Node.val <= 1000
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def min_depth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        if not root.left:
            return minDepth(root.right) + 1
        if not root.right:
            return minDepth(root.left) + 1
        return min(minDepth(root.right), minDepth(root.left)) +1
    def min_depth(self, root:Optional[TreeNode]) -> int:
        if not root:
            return 0;
        q = deque([root])
        depth = 1
        while q:
            for i in range(len(q)):
                node = q.popleft()
                if not node:
                    continue
                elif not (root.left or root.right):
                    return depth
                else:
                    q.append(root.left)
                    q.append(root.right)
                depth+=1
```
## binary-trees-dfs-02
1026. Maximum Difference Between Node and Ancestor
https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/description/
Given the root of a binary tree, find the maximum value v for which there exist different nodes a and b where v = |a.val - b.val| and a is an ancestor of b.

A node a is an ancestor of b if either: any child of a is equal to b or any child of a is an ancestor of b.

Example 1:
Input: root = [8,3,10,1,6,null,14,null,null,4,7,13]
Output: 7
Explanation: We have various ancestor-node differences, some of which are given below :
|8 - 3| = 5
|3 - 7| = 4
|8 - 1| = 7
|10 - 13| = 3
Among all possible differences, the maximum value of 7 is obtained by |8 - 1| = 7.
Example 2:
Input: root = [1,null,2,null,0,3]
Output: 3

Constraints:
The number of nodes in the tree is in the range [2, 5000].
0 <= Node.val <= 105
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxAncestorDiff(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        self.result = 0
        def helper(node, curr_max, curr_min):
            if not node:
                return
            self.result = max(self.result, abs(curr_max-node.val), abs(curr_min-node.val))
            curr_max = max(curr_max, node.val)
            curr_min = min(curr_min, node.val)
            helper(node.left, curr_max, curr_min)
            helper(node.right, curr_max, curr_min)
        helper(root, root.val, root.val)
        return self.result
```
## binary-trees-dfs-03
543. Diameter of Binary Tree
https://leetcode.com/problems/diameter-of-binary-tree/description/
Given the root of a binary tree, return the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

The length of a path between two nodes is represented by the number of edges between them.
Example 1:
Input: root = [1,2,3,4,5]
Output: 3
Explanation: 3 is the length of the path [4,2,1,3] or [5,2,1,3].
Example 2:
Input: root = [1,2]
Output: 1

Constraints:
The number of nodes in the tree is in the range [1, 104].
-100 <= Node.val <= 100
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
```
## binary-trees-dfs-04
100. Same Tree
https://leetcode.com/problems/same-tree/description/
## binary-trees-dfs-05
872. Leaf-Similar Trees
https://leetcode.com/problems/leaf-similar-trees/description/
## binary-trees-dfs-06
226. Invert Binary Tree
https://leetcode.com/problems/invert-binary-tree/description/
## binary-trees-dfs-07
101. Symmetric Tree
https://leetcode.com/problems/symmetric-tree/description/
## binary-trees-dfs-08
113. Path Sum II
https://leetcode.com/problems/path-sum-ii/description/
## binary-trees-dfs-09
1325. Delete Leaves With a Given Value
https://leetcode.com/problems/delete-leaves-with-a-given-value/description/
## binary-trees-dfs-10
437. Path Sum III
https://leetcode.com/problems/path-sum-iii/description/
## binary-trees-dfs-11
1372. Longest ZigZag Path in a Binary Tree
https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/description/