#### Question-1:

Given a root of a binary tree with n nodes, find its level order traversal.

#### Solution-1:

**Approach-1**
Create dictionary with keys as depth of the tree and append the tree data in its corrosponding Depth

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

Given a binary tree of size n, find its reverse level order traversal. ie- the traversal must begin from the last level.

#### Solution-2:

Same as above exect in Queue first insert right child then left child. Reverse the final list

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

```PY
maxDiameter = 0

def getDiameter(root):
    if root == None:
        return 0
    d1 = getDiameter(root.left)
    d2 = getDiameter(root.right)
    if maxDiameter < d1 + d2 +1:
        maxDiameter = d1 + d2 + 1
    return max(d1, d2) + 1

def diameter(root):
    maxDiameter = 0
    getDiameter(root, 0)
    return maxDiameter
```

#### Question-5

Given a binary tree, the task is to create a new binary tree which is a mirror image of the given binary tree.

#### Solution-5

swap left child and right child at every node

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
    Q = [[root,0]]

    min_lineNo = None
    max_lineNo = None

    while len(Q) >0:
        curr_obj = Q.pop(0)
        curr_lineNo = curr_obj[1]

        if min_lineNo == None or curr_lineNo < min_lineNo:
            min_lineNo = curr_lineNo

        if max_lineNo == None or curr_lineNo > max_lineNo:
            max_lineNo = curr_lineNo
        curr_node = curr_obj[0]

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

Same concept as in Top view (`The vertial line Concept`). Only change is that now in the dictionary replace the node at each level as and when new nodes comes. Henc in this way you will be getting last and the right most node (if level order traversal done from left to right).

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
        h1, b1 = is_tree_balanced(root.left)
        h2, b2 = is_tree_balanced(root.right)
        if abs(h2 - h1) >1:
            return max(h1,h2) + 1, 0
        else:
            return max(h1,h2) +1, b1 and b2

    def isBalanced(root):
        h,b = is_tree_balanced(root)
        return b
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

    left_node = get_leafNodes(root.left)
    right_node = get_leafNodes(root.right)

    return left_node + right_node

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

```PY
def get_DLL(root):
    if root == None:
        return None,None

    if root.left == None and root.right == None:
        return root,root

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

Solution-1

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

Solution-2

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

#### Solution-20

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
