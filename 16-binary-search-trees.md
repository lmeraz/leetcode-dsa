# search-trees
## search-trees-01
938.Range Sum of BST
## search-trees-01
Example 1:
938. Range Sum of BST
https://leetcode.com/problems/range-sum-of-bst/description/
Given the root node of a binary search tree and two integers low and high, return the sum of values of all nodes with a value in the inclusive range [low, high].
Example 1:
Input: root = [10,5,15,3,7,null,18], low = 7, high = 15
Output: 32
Explanation: Nodes 7, 10, and 15 are in the range [7, 15]. 7 + 10 + 15 = 32.
Example 2:
Input: root = [10,5,15,3,7,13,18,1,null,6], low = 6, high = 10
Output: 23
Explanation: Nodes 6, 7, and 10 are in the range [6, 10]. 6 + 7 + 10 = 23.
Constraints:
The number of nodes in the tree is in the range [1, 2 * 104].
1 <= Node.val <= 105
1 <= low <= high <= 105
All Node.val are unique.
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rangeSumBST(self, root, low, high):
        if not root:
            return 0
        ans = 0
        if low <= root.val <= high:
            ans+= root.val
        if low < root.val:
            ans += self.rangeSumBST(root.left, low, high)
        if root.val < high:
            ans+= self.rangeSumBST(root.right, low, high)
        return ans
```
## search-trees-02
Example 2:
530. Minimum Absolute Difference in BST
https://leetcode.com/problems/minimum-absolute-difference-in-bst/description/
Given the root of a Binary Search Tree (BST), return the minimum absolute difference between the values of any two different nodes in the tree.
Example 1:
Input: root = [4,2,6,1,3]
Output: 1
Example 2:
Input: root = [1,0,48,null,null,12,49]
Output: 1
Constraints:
The number of nodes in the tree is in the range [2, 104].
0 <= Node.val <= 105
Note: This question is the same as 783: https://leetcode.com/problems/minimum-distance-between-bst-nodes/
```python
class Solution:
    def getMinimumDifference(self, root: Optional[TreeNode]) -> int:
        def dfs(node):
            if not node:
                return
            left = dfs(node.left)
            values.append(node.val)
            right = dfs(node.right)
        values = []
        dfs(root)
        ans = float("inf")
        for i in range(1, len(values)):
            ans = min(ans, values[i] - values[i - 1])
        return ans
class Solution:
    def getMinimumDifference(self, root: Optional[TreeNode]) -> int:
        def iterative_inorder(root):
            stack = []
            values = []
            curr = root
            while stack or curr:
                if curr:
                    stack.append(curr)
                    curr = curr.left
                else:
                    curr = stack.pop()
                    values.append(curr.val)
                    curr = curr.right
            return values
        values = iterative_inorder(root)
        ans = float("inf")
        for i in range(1, len(values)):
            ans = min(ans, values[i] - values[i - 1])
        return ans
```
## search-trees-03
Example 3:
98. Validate Binary Search Tree
https://leetcode.com/problems/validate-binary-search-tree/
Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:
The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.

Example 1:
Input: root = [2,1,3]
Output: true
Example 2:
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.

Constraints:
The number of nodes in the tree is in the range [1, 104].
-231 <= Node.val <= 231 - 1
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def dfs(node):
            if not node:
                return
            left = dfs(node.left)
            values.append(node.val)
            right = dfs(node.right)
        values = []
        dfs(root)
        print(values)
        for i in range(1,len(values)):
            if values[i-1] >= values[i]:
                return False
        return True
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def dfs(node, small, large):
            if not node:
                return True
            if not (small < node.val < large):
                return False
            left = dfs(node.left, small, node.val)
            right = dfs(node.right, node.val, large)
            # tree is a BST if left and right subtrees are also BSTs
            return left and right
        return dfs(root, float("-inf"), float("inf"))
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        stack = [(root, float("-inf"), float("inf"))]
        while stack:
            node, small, large = stack.pop()
            if not (small < node.val < large):
                return False
            if node.left:
                stack.append((node.left, small, node.val))
            if node.right:
                stack.append((node.right, node.val, large))
        return True
```
## search-trees-04
701. Insert into a Binary Search Tree
https://leetcode.com/problems/insert-into-a-binary-search-tree/description/
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def insertIntoBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
```
## search-trees-05
270. Closest Binary Search Tree Value
https://leetcode.com/problems/closest-binary-search-tree-value/description/
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def closestValue(self, root: Optional[TreeNode], target: float) -> int:
```
## search-trees-06
700. Search in a Binary Search Tree
https://leetcode.com/problems/search-in-a-binary-search-tree/description/
```python
```
## search-trees-07
1305. All Elements in Two Binary Search Trees
https://leetcode.com/problems/all-elements-in-two-binary-search-trees/description/
## search-trees-08
235. Lowest Common Ancestor of a Binary Search Tree
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/
## search-trees-09
450. Delete Node in a BST
https://leetcode.com/problems/delete-node-in-a-bst/description/
