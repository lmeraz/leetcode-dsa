
trees and graphs
abstract data structures
node
- stores data
- stores a pointer

graph - any colletion of nodes and pointers to other noeds

nodes of graphs = vertices

pointers that connect - edges

binary tree - max 2 childenr left/right child

root = top of tree
parent -> child
leaf node no children
depth - how far from the root node

Implement a tree

```python
class TreeNode:
    def __init__(self, val, left, right):
        self.val = val
        self.left = left
        self.right = right
```


```python
def dfs(node):
    if node == None:
        return

    dfs(node.left)
    dfs(node.right)
    return
```


The name of each traversal is describing when the current node's logic is performed.

Pre -> before children

In -> in the middle of children

Post -> after children


time complexity is always n total number of nodes
if there is k work at each node
O(n*k) 

For space complexity, even if you are using recursion, the calls are still placed on the call stack which counts as extra space. The largest the stack will be (for either iterative or recursive) at any time will depend on the tree. For recursion, in the worst case it is 
O(n) if the tree is just a straight line, so usually, the correct answer to give for space complexity is 
O(n). If the tree is "complete" (all nodes have 0 or 2 children and each level except the last is full), then the space complexity is
O(logn), but this is a best-case scenario.


binary trees
depth first search

breadth first search

depth first search
traverse as far down the tree as possible
until reaching the leaf node before considering another direction
typically uses recursion though stack can be used
preorder
inorder
postorder



binary trees bfs
traverse all noders at a given depth before moving on to the next depth
complete binary tree - every level except possibly last is full

dfs/bfs interchangeably since you will visit every node


dfs disatvantage
- wasting a lot of time lookijng up a value if the node is in the one to the right

bfs disadvantage
- if node is at the bottom

dfs uses space linear with height of tree

bfrs uses space linear with leveler that has most nodes

binary search trees
binary search tree:
all values in its left subtree are less than the value in the node and all values in its right subtree are greater than the value in the done

this implies bst musst be unique

trivia an in order dfs traversal prioritizing left before right on a bst will handle the nodes in a sorted order

