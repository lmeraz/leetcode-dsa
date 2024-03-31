# bfs
## bfs-01
Print all nodes using a BFS approach
https://leetcode.com/explore/interview/card/leetcodes-interview-crash-course-data-structures-and-algorithms/707/traversals-trees-graphs/4619/
```python
from collections import deque
def print_all_nodes(root):
    queue = deque([root])
    while queue:
        nodes_in_current_level = len(queue)
        # do some logic here for the current level
        for _ in range(nodes_in_current_level):
            node = queue.popleft()
            # do some logic here on the current node
            print(node.val)
            # put the next level onto the queue
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
```
## bfs-02
Example 1:
199. Binary Tree Right Side View
https://leetcode.com/problems/binary-tree-right-side-view/description/
Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Example 1:
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]

Example 2:
Input: root = [1,null,3]
Output: [1,3]

Example 3:
Input: root = []
Output: []

Constraints:
The number of nodes in the tree is in the range [0, 100].
-100 <= Node.val <= 100
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        ans = []
        if not root:
            return ans
        queue = deque([root])
        while queue:
            nodes_in_current_level = len(queue)
            ans.append(queue[-1].val)
            is_new_level = True
            for _ in range(nodes_in_current_level):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        return ans
```
## bfs-03
Example 2:
515. Find Largest Value in Each Tree Row
https://leetcode.com/problems/find-largest-value-in-each-tree-row/description/
Given the root of a binary tree, return an array of the largest value in each row of the tree (0-indexed).

Example 1:
Input: root = [1,3,2,5,3,null,9]
Output: [1,3,9]

Example 2:
Input: root = [1,2,3]
Output: [1,3]
Constraints:
The number of nodes in the tree will be in the range [0, 104].
-2^31 <= Node.val <= 2^31 - 1
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        ans = []
        if not root:
            return ans
        queue = deque([root])
        while queue:
            current_length = len(queue)
            curr_max = float("-inf")
            for _ in range(current_length):
                node = queue.popleft()
                curr_max = max(curr_max, node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            ans.append(curr_max)
        return ans
```
## bfs-04
1302. Deepest Leaves Sum
https://leetcode.com/problems/deepest-leaves-sum/editorial/
Given the root of a binary tree, return the sum of values of its deepest leaves.
Example 1:
Input: root = [1,2,3,4,5,null,6,7,null,null,null,null,8]
Output: 15
Example 2:
Input: root = [6,7,8,2,7,1,3,9,null,1,4,null,null,null,5]
Output: 19

Constraints:
The number of nodes in the tree is in the range [1, 104].
1 <= Node.val <= 100
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def deepestLeavesSum(self, root: Optional[TreeNode]) -> int:
        ans = 0
        if not root:
            return ans
        queue = deque([root])
        while queue:
            ans = 0
            current_length = len(queue)
            for _ in range(current_length):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
                ans+=node.val
        return ans
```
## bfs-05
103. Binary Tree ZigZag Order Traversal
https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/
Given the root of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

Example 1:
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]

Example 2:
Input: root = [1]
Output: [[1]]

Example 3:
Input: root = []
Output: []

Constraints:
The number of nodes in the tree is in the range [0, 2000].
-100 <= Node.val <= 100
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        ans = []
        if not root:
            return []
        queue = deque([root])
        odd = True
        while queue:
            nodes_at_current_level = len(queue)
            temp = []
            for _ in range(nodes_at_current_level):
                node = queue.popleft()
                temp.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            if odd:
                ans.append(temp)
            else:
                ans.append(reversed(temp))
            odd = not odd
        return ans
```
