#### Question-1:

Given a root of a binary tree with n nodes, find its level order traversal.

#### Solution-1:

**Approach-1**
Create dictionary with keys as depth of the tree and append the tree data in its corrosponding Depth. [Recursive solution]

Time Complexity: O(n) \
Space Complexity: O(n)

```PY
def getLevelOrder(root, depth, result):

    if root == None:
        return result

    if depth in result:
        result[depth].append(root.data)
    else:
        result[depth] = [root.data]

    getLevelOrder(root.left, depth + 1, result)
    getLevelOrder(root.right, depth + 1, result)

    return result

def levelOrder(root):
    depth = 0
    result = {}
    getLevelOrder(root, depth,result)
    depth = 0
    final_list = []
    while True:
        if depth in result:
            final_list = final_list + result[depth]
        else:
            break
        depth +=1
    return final_list
```

**Approach-2**
create a function which can print all the node at a given height. Call this function for all the height from h = 0 till no data is found.

Time Complexity: O($n^2$) \
Space Complexity: O(n)

**Approach-3**
create Queue data structure, store the node's children before printing its data. pop a node from queue and repeat

Time Complexity: O(n) \
Space Complexity: O(n)

```PY
def levelOrder(root):
    if root == None:
        return []

    Q = [root]
    final_list = []
    while len(Q) >0:
        curr_node = Q.pop(0)
        final_list.append(curr_node.data)

        if curr_node.left:
            Q.append(curr_node.left)
        if curr_node.right:
            Q.append(curr_node.right)

    return final_list
```

#### Question-2:

Given a binary tree of size n, find its reverse level order traversal. ie- the traversal must begin from the last level from left to right.

#### Solution-2:

Same as above exect in Queue first insert right child then left child. Store all the values in the list and finally Reverse the list

```PY
def reverseLevelOrder(root):
    if root == None:
        return []

    Q = [root]
    result = []
    while len(Q):
        curr_node = Q.pop(0)
        result.append(curr_node.data)

        if curr_node.right:
            Q.append(curr_node.right)

        if curr_node.left:
            Q.append(curr_node.left)

    result.reverse()
    return result
```

#### Question-3:

Given a binary tree, find its height.

#### Solution-3:

Do Recursive traversal

1. Get left subtree height
2. Get right subtree height
3. return `max(left_height, right_height) + 1`

```PY
def treeHeight(root, h):
    if root == None:
        return 0

    h1 =  treeHeight(root.left, h + 1)
    h2 =  treeHeight(root.right, h + 1)

    return max(h1 + 1, h2 + 1)
```

#### Question-4:

The diameter of a tree (sometimes called the width) is the number of nodes on the longest path between two end nodes. Find the Diameter of a Tree.

#### Solution-4:

Do Recursive traversal

1. Get left subtree height
2. Get right subtree height
3. mentain `diameter_value` as global variable
4. if `left_height + right_height + 1 < diameter_value` then update `diameter_value`
5. return `max(left_height, right_height) + 1`

```PY
maxDiameter = 0

def getDiameter(root):
    if root == None:
        return 0
    h1 = getDiameter(root.left)
    h2 = getDiameter(root.right)
    if maxDiameter < h1 + h2 +1:
        maxDiameter = h1 + h2 + 1
    return max(h1, h2) + 1

def diameter(root):
    maxDiameter = 0
    getDiameter(root)
    return maxDiameter
```

#### Question-5

Given a binary tree, the task is to create a new binary tree which is a mirror image of the given binary tree.

#### Solution-5

swap left child and right child at every node

```PY
def getDiameter(root):
    if root == None:
        return None

    if root.left == None and root.right == None:
        return root

    left_tree = getDiameter(root.left)
    right_tree = getDiameter(root.right)

    root.left = right_tree
    root.right = left_tree

    return root
```

#### Question-6

Given a Binary Tree, return Left view of it. Left view of a Binary Tree is set of nodes visible when tree is visited from Left side.

#### Solution-6

Do level order traversal and at every level print the first element

```PY
def LeftView(root):
    if root == None:
        return []

    Q = [root, None]
    final_list = [root.data]

    while len(Q) > 0:
        curr_node = Q.pop(0)

        if curr_node == None:
            if len(Q) == 0:
                break
            Q.append(None)
            curr_node = Q.pop(0)
            final_list.append(curr_node.data)

        if curr_node.left != None:
            Q.append(curr_node.left)
        if curr_node.right != None:
            Q.append(curr_node.right)

    return final_list
```

#### Question-7

Given a Binary Tree, find Right view of it. Right view of a Binary Tree is set of nodes visible when tree is viewed from right side.

#### Solution-7

Do level order traversal first insert right node and then left node in the Queue at every level print the first element of each level

```PY
def rightView(root):
    if root == None:
        return []

    Q = [root, None]
    final_list = [root.data]

    while len(Q) > 0:
        curr_node = Q.pop(0)
        if curr_node == None:
            if len(Q) == 0:
                break
            Q.append(None)
            curr_node = Q.pop(0)
            final_list.append(curr_node.data)

        if curr_node.right != None:
            Q.append(curr_node.right)
        if curr_node.left != None:
            Q.append(curr_node.left)

    return final_list
```

#### Question-8

Given below is a binary tree. The task is to print the top view of binary tree. Top view of a binary tree is the set of nodes visible when the tree is viewed from the top.

#### Solution-8

Do level order traversal and mentain the ` vertical Line Number` for each node(like -2 -1 0 1 2 etc.). create a dictionary which stores the first node data found in respective vertial line number.

```PY
def topView(root):
    if root == None:
        return []

    final_list = []
    object_list = {}
    # [[Root Node, vertial Line No]]
    Q = [[root,0]]

    min_lineNo = None
    max_lineNo = None

    while len(Q) >0:
        curr_obj = Q.pop(0)
        curr_lineNo = curr_obj[1]
        curr_node = curr_obj[0]

        if min_lineNo == None or curr_lineNo < min_lineNo:
            min_lineNo = curr_lineNo

        if max_lineNo == None or curr_lineNo > max_lineNo:
            max_lineNo = curr_lineNo

        if curr_lineNo not in object_list:
            object_list[curr_lineNo] = curr_node.data

        if curr_node.left != None:
            Q.append([curr_node.left, curr_lineNo - 1])

        if curr_node.right != None:
            Q.append([curr_node.right, curr_lineNo + 1])

    for i in range (min_lineNo, max_lineNo +1):
        final_list.append(object_list[i])

    return final_list
```

#### Question-9

Given a binary tree, print the bottom view from left to right. A node is included in bottom view if it can be seen when we look at the tree from bottom. If two nodes are at the same place take the right node.

#### Solution-9

Same concept as in Top view (`The vertial line Concept`). Only change is that now in the dictionary replace the node at each level as and when new nodes comes. Hence in this way you will be getting last and the right most node (if level order traversal done from left to right).

```PY
def bottomView(root):
    if root == None:
        return []

    Q = [[root,0]]
    final_list = []
    object_list = {}
    min_lineNo = None
    max_lineNo = None

    while len(Q)>0:
        curr_obj = Q.pop(0)
        curr_line = curr_obj[1]
        curr_node =  curr_obj[0]

        if min_lineNo == None or curr_line < min_lineNo:
            min_lineNo = curr_line
        if max_lineNo == None or curr_line > max_lineNo:
            max_lineNo = curr_line

        object_list[curr_line] = curr_node.data

        if curr_node.left != None:
            Q.append([curr_node.left, curr_line - 1])
        if curr_node.right != None:
            Q.append([curr_node.right, curr_line + 1])

    for i in range(min_lineNo, max_lineNo + 1):
        final_list.append(object_list[i])

    return final_list
```

#### Question-10

Given a binary tree with n nodes. Find the zig-zag level order traversal of the binary tree. In zig zag traversal starting from the first level go from left to right for odd-numbered levels and right to left for even-numbered levels.

#### Solution-10

It is same as level order traversal except mentain one flag which is true at alternate levels. For levels having flag true reverse that level before storing in final list.

```PY
def zigZagTraversal(root):
    if root == None:
        return []

    Q = [root, None]
    isReversed = False
    final_list = []
    level_list = list()
    while len(Q):
        curr_node = Q.pop(0)

        if curr_node == None:
            if isReversed:
                level_list.reverse()
                final_list = final_list + level_list
                isReversed = False
            else:
                final_list = final_list + level_list
                isReversed = True
            if len(Q) == 0:
                break
            level_list = list()
            Q.append(None)
            curr_node = Q.pop(0)

        level_list.append(curr_node.data)

        if curr_node.left != None:
            Q.append(curr_node.left)
        if curr_node.right != None:
            Q.append(curr_node.right)

    return final_list
```

#### Question-11

Given a binary tree, find if it is height balanced or not. A tree is height balanced if difference between heights of left and right subtrees is not more than one for all nodes of tree.

#### Solution-11

Logic is similar to finding getting height at each node from left and right and the comparing if its left and right child is balanced or not.

```PY
def is_tree_balanced(root):
        if root == None:
            return 0,1   # Height, Balanced or not
        h1, is_balanced1 = is_tree_balanced(root.left)
        h2, is_balanced2 = is_tree_balanced(root.right)
        if abs(h2 - h1) > 1:
            return max(h1, h2) + 1, 0
        else:
            return max(h1, h2) + 1, is_balanced1 and is_balanced2

    def isBalanced(root):
        height, is_balanced = is_tree_balanced(root)
        return is_balanced
```

#### Question-12

Given a Binary Tree, print the diagonal traversal of the binary tree.

#### Solution-12

Print the right child and store its left child in the Queue. pop one element from Queue and repeat the same process.

```PY
def diagonal(root):
    if root == None:
        return []
    Q = [root]
    final_list = []

    while len(Q) >0:
        curr_node = Q.pop(0)
        temp = curr_node
        while temp:
            final_list.append(temp.data)
            if temp.left != None:
                Q.append(temp.left)

            temp = temp.right

    return final_list
```

#### Question-13

Given a Binary Tree, find its Boundary Traversal. The traversal should be in the following order:

1. Left boundary nodes: defined as the path from the root to the left-most node ie. the leaf node you could reach when you always travel preferring the left subtree over the right subtree.
2. Leaf nodes: All the leaf nodes except for the ones that are part of left or right boundary.
3. Reverse right boundary nodes: defined as the path from the right-most node to the root. The right-most node is the leaf node you could reach when you always travel preferring the right subtree over the left subtree. Exclude the root from this as it was already included in the traversal of left boundary nodes.

#### Solution-13

Boundary Traversal = left_boundary node + leaf node + right_boundary node in reverse order

```PY
# To get the leaf node
def get_leafNodes(root):
    if root == None:
        return []
    if root.left == None and root.right == None:
        return [root.data]

    left_leaf = get_leafNodes(root.left)
    right_leaf = get_leafNodes(root.right)

    return left_leaf + right_leaf

# Main Solution
def printBoundaryView(root):
    if root == None:
        return []

    left_boundary = []
    right_boundary = []
    leaf_nodes = []

    # get left baoundary without root
    temp = root.left
    while temp != None and (temp.left != None or temp.right != None):
        left_boundary.append(temp.data)
        if temp.left != None:
            temp = temp.left
        else:
            temp = temp.right

    # get right baoundary without root
    temp = root.right
    while temp != None and (temp.left != None or temp.right != None):
        right_boundary.append(temp.data)
        if temp.right != None:
            temp = temp.right
        else:
            temp = temp.left

    # get leaf node
    if root.left != None or root.right != None:
        leaf_nodes = get_leafNodes(root)

    # Reverse the right boundary
    right_boundary.reverse()

    # Combine the result
    return  [root.data] + left_boundary + leaf_nodes + right_boundary
```

#### Question-14

Construct a binary tree from a string consisting of parenthesis and integers. The whole input represents a binary tree. It contains an integer followed by zero, one or two pairs of parenthesis. The integer represents the roots value and a pair of parenthesis contains a child binary tree with the same structure. \
Example:

```PY
Input: "4(2(3)(1))(6(5))"
Output:
           4
         /   \
        2     6
       / \   /
      3   1 5
```

#### Solution-14

`Method-1:` Create root node, get left sub tree string and right sub tree string. recursively traverse left and right.

Time complexity: $O(n^2)$

`Method-2:` Create root node, if `(` go right else if ')' return if again `(` go left. For this solution mentain the global index

Time complexity: $O(n)$

**Method-1**

```PY
def get_LeftRight_str(str):
        if len(str) == 0:
            return  "", ""

        start_index = -1
        stop_index = -1
        flag = True
        stack1 = []

        for i in range(len(str)):
            if str[i] == '(':
                stack1.append(str[i])
                if flag == True:
                    start_index = i+1
                    flag = False

            elif str[i] == ')':
                stack1.pop()

            if len(stack1) == 0:
                stop_index = i - 1
                break

        if start_index < len(str) and stop_index >= 0:
            str1 = str[start_index: stop_index +1]
        else:
            str1 = ""
        stack2 = []
        flag = True
        start_index = -1
        stop_index = -1

        for j in range(i+1, len(str)):
            if str[j] == '(':
                stack2.append(str[j])
                if flag == True:
                    start_index = j+1
                    flag = False

            elif str[j] == ')':
                stack2.pop()

            if len(stack2) == 0:
                stop_index = j - 1
                break

        if start_index < len(str) and stop_index >= 0:
            str2 = str[start_index: stop_index +1]
        else:
            str2 = ""
        return str1, str2


    def getNode(val):
        return Node(val)

    def get_tree(str):
        if len(str) == 0:
            return None

        val = ""
        for i in range(len(str)):
            if str[i].isdigit():
                val += str[i]
            else:
                break

        rootNode = getNode(val)
        left_str, right_str =  get_LeftRight_str(str[i:])

        if left_str != "":
            if left_str.isdigit():
                rootNode.left = getNode(left_str)
            else:
                rootNode.left = get_tree(left_str)

        if right_str != "":
            if right_str.isdigit():
                rootNode.right = getNode(right_str)
            else:
                rootNode.right = get_tree(right_str)

        return rootNode

    def treeFromString(s):

        if len(s) == 0 or s[0].isdigit() == False:
            return getNode(0)

        rootNode = get_tree(s)

        return rootNode
```

Time Complexity: $O(n^2)$

**Method-2**

```PY
index = 0
def getNode(val):
    return Node(val)

def get_tree(str):
    if index >= len(str):
        return None

    val = ""
    count = 0
    for i in range(index, len(str)):

        if str[i].isdigit():
            val += str[i]
            count +=1
        else:
            break

    if val == "":
        rootNode = None
    else:
        rootNode = getNode(val)

    index += count
    if index == len(str) or str[index] == ')':
        index +=1
        return rootNode

    if str[index] == '(':
        index +=1
        rootNode.left = get_tree(str)

    if index >= len(str):
        return rootNode

    if str[index] == '(':
        index +=1
        rootNode.right = get_tree(str)

    index +=1
    return rootNode

    def treeFromString(s):

        if len(s) == 0 or s[0].isdigit() == False:
            return getNode(0)

        return get_tree(s)
```

Time complexity: $O(n)$

#### Question-15

Given a Binary Tree (BT), convert it to a Doubly Linked List(DLL) In-Place. The order of nodes in DLL must be same as Inorder of the given Binary Tree

#### Solution-15

Do recusrive traversal

1. Get head and tail of left and right subtree
2. Create DLL for root, left subtree and right sub tree
3. return the DLL

```PY
def get_DLL(root):
    if root == None:
        return None, None

    if root.left == None and root.right == None:
        return root, root  # returning Tail, Head which is same

    LHead, LTail = get_DLL(root.left)
    RHead, RTail = get_DLL(root.right)

    root_head = root
    root_tail = root

    root.left = LTail
    root.right = RHead

    if (LTail != None):
        LTail.right = root
        root_head = LHead


    if RHead != None:
        RHead.left = root
        root_tail = RTail


    return root_head, root_tail
```

#### Question-16

Given a Binary Tree of size N , where each node can have positive or negative values. Convert this to a tree where each node contains the sum of the left and right sub trees of the original tree. The values of leaf nodes are changed to 0.

```PY
Input:
             10
          /      \
        -2        6
       /   \     /  \
     8     -4   7    5

Output:
            20
          /    \
        4        12
       /  \     /  \
     0     0   0    0
```

#### Solution-16

```PY
def get_sum(root):
    if root == None:
        return 0 ,0

    if root.left == None and root.right == None:
        temp = root.data
        root.data = 0
        return root.data, temp

    sum1, val1 = get_sum(root.left)
    sum2, val2 =  get_sum(root.right)

    temp = root.data
    root.data = sum1 + val1 + sum2 + val2

    return root.data, temp
```

#### Question-17

Given an array A[] which represents a Complete Binary Tree i.e, if index i is the parent, index 2i + 1 is the left child and index 2i + 2 is the right child.
The task is to find the minimum number of swaps required to convert it into a Binary Search Tree.

#### Solution-17

**Theory**

Lets understand how minim swaps required to sort an array works

```
input: 5, 0, 4, 2, 1, 3

SET(value, index) => (5, 0) (0, 1) (4, 2) (2, 3) (1, 4) (3, 5)

Sorted order: (1, 4) (2, 3) (3, 5) (4, 2) (5, 0)

Instead of finding the swaps needed to sort the list,
find the minimum swaps required to convert the sorted list
back to the original list (as both approaches yield the same result).

Pick any element 𝐸𝑖, swap it with the element at the
𝑖-th index, and repeat until the index matches 𝑖.
Then, pick the next element and continue. next element.

ALGORITHM
--------
total_swaps = 0
for i in range(len(A)):
    curr_index = A[i][1]
    if i == curr_index:
        continue
    swap(A[i], A[curr_index])
    total_swaps = total_swaps + 1
    # Do not increament i untill i == curr_index
    i = i - 1
```

Note

1. This algoritm is not restricted to sorting, you can find minimum swaps where target list is in any specific order (sorted in our case)
2. If a list contains a continuous range of numbers, you can sort it in O(n) time complexity using the following algorithm: \
    Example: -2, 4, -1, 3, 0, 2, 1

   1. Subtract each element from the largest number in the list.

   Result: 6, 0, 5, 1, 4, 2, 3

   2. Instead of swapping based on index, swap based on values to get the sorted list.
   3. Finally, add the largest number to each element.

**Solution**

If given binary tree is BST then its in-order traversel will be sorted. Hence solution boils down to

1. Find the in-order traversal and store in array
2. Find the minimum swaps required to sort the array
3. We observe that given input list will always be sorted

```PY
def inOrderTraversal(arr, i,inorder_list):
    if i >= len(arr):
        return
    inOrderTraversal(arr, 2*i + 1,inorder_list)
    inorder_list.append([i, arr[i]])
    inOrderTraversal(arr, 2*i + 2,inorder_list)

def getMinSwaps(inorder_list):

    count = 0
    total_swaps = 0

    for i in range(len(inorder_list)):
        curr_pair = inorder_list[i]

        if i == curr_pair[0]:
            continue

        while i != curr_pair[0]:
            temp = curr_pair
            curr_pair = inorder_list[temp[0]]
            inorder_list[temp[0]] = temp
            total_swaps +=1


    return total_swaps
```

**Note:** If input list is not sorted then above code will slightly change as follows.

1. Sort the input list and determine the minimum swaps required in this step.
2. Obtain the inorder list from the sorted list and find the minimum swaps needed to make the inorder list sorted.
3. Sum the total swaps made in the above two steps.

#### Question-18

Given a Binary Tree. Return true if, for every node X in the tree other than the leaves, its value is equal to the sum of its left subtree's value and its right subtree's value. Else return false.

```PY
Input:
    3
  /   \
 1     2

Output: 1
Explanation:
The sum of left subtree and right subtree is
1 + 2 = 3, which is the value of the root node.
Therefore,the given binary tree is a sum tree.
```

#### Solution-18

Perform a recursive traversal. Get the sum of the left subtree and the right subtree. If the sums match, return the total sum; otherwise, return -1.

```PY
def checkSum(root):
    if root == None:
        return 0

    if root.left == None and root.right == None:
        return root.data

    s1 = checkSum(root.left)
    s2 = checkSum(root.right)

    if s1 == -1 or s2 == -1 or s1 + s2 != root.data:
        return -1
    else:
        return s1 + s2 + root.data

def isSumTree(root):
    val = checkSum(root)
    if val <=0:
        return False
    else:
        return True
```

#### Question-19

Given a binary tree with n nodes, determine whether all the leaf nodes are at the same level or not. Return true if all leaf nodes are at the same level, and false otherwise.

```
Input Tree:

    10
   /  \
 20   30
 /  \
 10   15

Output: false
Explanation: The binary tree has a height of 3 and the leaves are not at the same level.
```

#### Solution-19

**Recursive Solution**

For every node, if both its left and right subtrees exist, their heights must be exactly the same.

```PY
def get_flag(root):
    if root == None:
        return 0

    h1 = get_flag(root.left)
    h2 = get_flag(root.right)

    if h1 == -1 or h2 == -1:
        return -1

    if root.left == None or root.right == None:
        return max(h1, h2) + 1

    if h1 != h2:
        return -1
    else:
        return max(h1,h2) + 1

def check(root):
    val = get_flag(root)
    if val <0:
        return False
    else:
        return True
```

**Iterative Solution** \
Every leaf node should have the same height. Perform a level order traversal while keeping track of the height at each level. When the first leaf is encountered, update the leaf_height. For every subsequent leaf, check if its height matches leaf_height.

```PY
def check(root):
    if root == None:
        return True

    Q = [root,None]
    leaf_height = -1
    height = 0

    while len(Q) >0:
        curr_node = Q.pop(0)
        if curr_node == None:
            height +=1
            if len(Q) == 0:
                break

            Q.append(None)
            curr_node = Q.pop(0)

        if curr_node.left == None and curr_node.right == None:
            if leaf_height == -1:
                leaf_height = height

            elif leaf_height != height:
                return False

        if curr_node.left !=None:
            Q.append(curr_node.left)

        if curr_node.right !=None:
            Q.append(curr_node.right)

    return True
```

#### Question-20

Given a binary tree having n nodes. Find the sum of all nodes on the longest path from root to any leaf node. If two or more paths compete for the longest path, then the path having maximum sum of nodes will be considered.

```
Input:
         4
       /   \
      2     5
     / \   / \
    7   1 2   3
       /
      6

Output: (4 + 2 + 1 + 6) = 13
```

#### Solution-20

Perform a recursive traversal to get the sum and height of the left subtree and the right subtree. Based on the heights, return the results.

```PY
def get_longestPathSum(root):
    if root == None:
        return 0,0

    if root.left == None and root.right == None:
        return root.data, 1


    lSum, lHeight = get_longestPathSum(root.left)
    rSum, rHeight = get_longestPathSum(root.right)

    if lHeight > rHeight:
        return lSum + root.data, lHeight + 1
    elif lHeight < rHeight:
        return rSum + root.data, rHeight + 1
    else:
        return max(lSum, rSum) + root.data, lHeight + 1

def sumOfLongRootToLeafPath(root):
    sum, height = get_longestPathSum(root)
    return sum
```
